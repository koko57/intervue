<template>
  <layout>
    <template v-slot:main>
      <h3>Add new question</h3>
      <input
        aria-label="Question"
        type="text"
        v-model="question"
        placeholder="Question"
      />
      <textarea
        aria-label="Answer"
        v-model="answer"
        placeholder="Answer (can be added/edited later)"
      />
      <!--      TODO: add select for levels-->
      <!--      <select v-model="level">-->
      <!--        <option disabled value="">Please select one</option>-->
      <!--        <option>Mid</option>-->
      <!--        <option>Senior</option>-->
      <!--      </select>-->
      <button v-on:click="addNew">Add</button>
    </template>
  </layout>
</template>

<script>
import { db } from "../config/firebase";
import BaseLayout from "../components/BaseLayout";
export default {
  name: "add-new",
  components: {
    layout: BaseLayout
  },
  data() {
    return {
      question: "",
      answer: "",
      level: ""
    };
  },
  methods: {
    addNew: function() {
      db.collection("questions")
        .add({
          question: this.question,
          answer: this.answer
        })
        .then(() => this.$router.push("/"));
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
button {
  margin-top: 20px;
  width: 10%;
  cursor: pointer;
}
</style>
