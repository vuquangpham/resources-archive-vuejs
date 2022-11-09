<template>
  <BaseDialog
    @close="inputIsValid = true"
    v-if="!inputIsValid"
    title="Invalid Input"
  >
    <template v-slot:default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Please check all inputs!</p>
    </template>
    <template v-slot:actions>
      <BaseButton @click="inputIsValid = true">Okay</BaseButton>
    </template>
  </BaseDialog>
  <BaseCard>
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="title">Title</label>
        <input id="title" type="text" v-model="title" />
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <textarea id="description" rows="5" ref="descriptionInput"></textarea>
      </div>
      <div class="form-group">
        <label for="link">Link</label>
        <input id="link" type="text" v-model="link" />
      </div>
      <div class="form-group">
        <BaseButton type="submit">Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>
</template>

<script>
import BaseCard from "../UI/BaseCard.vue";
import BaseButton from "../UI/BaseButton.vue";
import BaseDialog from "../UI/BaseDialog.vue";

export default {
  components: {
    BaseCard,
    BaseButton,
    BaseDialog,
  },
  data() {
    return {
      title: "",
      link: "",
      inputIsValid: true,
    };
  },
  inject: ["submit"],
  methods: {
    handleSubmit() {
      const descriptionInput = this.$refs.descriptionInput.value;
      if (!this.title || !descriptionInput || !this.link) {
        this.inputIsValid = false;
        return;
      }
      console.log(descriptionInput);
      this.submit({
        title: this.title,
        description: descriptionInput,
        link: this.link,
      });

      // reset input
      this.title = "";
      this.link = "";
      this.$refs.descriptionInput.value = "";
    },
  },
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

.form-group {
  margin: 1rem 0;
}
</style>
