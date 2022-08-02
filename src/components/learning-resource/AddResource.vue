<template>
  <base-dialog
    v-if="inputIsInvalid"
    @close="confirmError"
    title="Invalid Input"
  >
    <template #default>
      <p>You are not allowed to submit empty inputs</p>
      <p>Please recheck all inputs and fill them all</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" ref="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          ref="description"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="text" name="link" id="link" ref="link" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
  components: { BaseButton },
  inject: ['addData'],
  data() {
    return {
      title: '',
      description: '',
      link: '',
      inputIsInvalid: false
    };
  },
  methods: {
    submitResource() {
      const title = this.$refs.title.value;
      const description = this.$refs.description.value;
      const link = this.$refs.link.value;
      if (
        title.trim() === '' ||
        description.trim() === '' ||
        link.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addData(title, description, link);
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
};
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
