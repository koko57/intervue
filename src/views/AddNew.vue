<template>
  <base-layout v-bind:showNavbar="true">
    <template>
      <h3>Add a new question</h3>
      <form-input
        aria-label="Question"
        type="text"
        v-model="question"
        placeholder="Question"
      />
      <span v-if="error" class="error">Question is required!</span>
      <textarea
        aria-label="Answer"
        v-model="answer"
        placeholder="Answer (can be added/edited later)"
      />
      <filter-select v-model="filters" />
      <button v-on:click="validateAndSubmit">Add</button>
    </template>
  </base-layout>
</template>

<script>
import { db, auth } from "@/config/firebase";
import BaseLayout from "@/components/BaseLayout";
import FormInput from "@/components/FormInput";
import FilterSelect from "@/components/FilterSelect";

export default {
  name: "AddNew",
  components: {
    FilterSelect,
    FormInput,
    BaseLayout
  },
  data() {
    return {
      question: "",
      answer: "",
      filters: { level: "", category: "" },
      error: false
    };
  },
  methods: {
    addNew() {
      db.collection("questions")
        .add({
          question: this.question,
          answer: this.answer,
          createdAt: new Date(),
          createdBy: auth.currentUser.email.split("@")[0],
          ...this.filters
        })
        .then(() => this.$router.push("/"));
    },
    validateAndSubmit() {
      if (!this.question) {
        this.error = true;
      } else {
        this.error = false;
        this.addNew();
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/variables";
@import "../styles/mixins";

textarea {
  margin: 10px auto;
  width: 90%;
  padding: 1rem;
  @include border;
}
.error {
  color: $color-pink;
  font-size: 0.9rem;
}
button {
  margin-top: 20px;
  min-width: 100px;
  cursor: pointer;
}
</style>
