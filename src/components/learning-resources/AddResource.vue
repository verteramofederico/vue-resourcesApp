<template>
  <div>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template v-slot:default>
        <p>At least one input value in invalid</p>
        <p>Please enter a correct input</p>
    </template>
    <template v-slot:actions>
        <base-button @click="confirmError">Okay</base-button>
    </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
            <label for="title">title</label>
            <input id="title" name="title" type="text" ref="titleInput">
            </div>
            <div class="form-control">
            <label for="description">description</label>
            <textarea id="description" name="descripton" rows="3" ref="descInput"></textarea>
            </div>
            <div class="form-control">
            <label for="link">Link</label>
            <input id="link" name="link" type="text" ref='linkInput'>
            </div>
            <div>
                <base-button type="submit">Add resource</base-button>
            </div>
        </form>
    </base-card>
    </div>
</template>

<script>
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog },
    inject: ['addResource'],
    data () {return {
      inputIsInvalid: false
    }},
    methods: {
        submitData () {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.descInput.value;
            const enteredUrl = this.$refs.linkInput.value;

        if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
        this.addResource(enteredTitle, enteredDescription, enteredUrl)
        this.$refs.titleInput.value === ""
        },
        confirmError() {
          this.inputIsInvalid = false
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>