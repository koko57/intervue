<template>
  <layout v-bind:showNavbar="true">
    <template>
      <h3>Add new question</h3>
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
      <!--      <select v-model="level">-->
      <!--        <option disabled value="">Please select one</option>-->
      <!--        <option>Mid</option>-->
      <!--        <option>Senior</option>-->
      <!--      </select>-->
      <!--      <select v-model="category">-->
      <!--        <option disabled value="">Please select one</option>-->
      <!--        <option>JavaScript</option>-->
      <!--        <option>CSS</option>-->
      <!--        <option>HTML</option>-->
      <!--        <option>General</option>-->
      <!--      </select>-->
      <button v-on:click="validateAndSubmit">Add</button>
    </template>
  </layout>
</template>

<script>
import { db, auth } from "../config/firebase";
import BaseLayout from "../components/BaseLayout";
import FormInput from "../components/FormInput";
export default {
  name: "add-new",
  components: {
    FormInput,
    layout: BaseLayout
  },
  data() {
    return {
      question: "",
      answer: "",
      level: "",
      category: "",
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
          createdBy: auth.currentUser.email.split("@")[0]
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

<style scoped>
input,
textarea {
  margin: 10px auto;
  width: 90%;
  padding: 15px;
  border: 1px solid #eee;
  border-radius: 0.5rem;
}
.error {
  color: #cd6183;
  font-size: 0.9rem;
}
button {
  margin-top: 20px;
  min-width: 100px;
  cursor: pointer;
}
</style>
