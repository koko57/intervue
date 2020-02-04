<template>
  <div class="login">
    <h3>Add new question</h3>
    <input type="text" v-model="question" placeholder="Q" /><br />
    <textarea v-model="answer" placeholder="A" /><br />
    <button @click="addNew">Add</button>
  </div>
</template>

<script>
import { db } from "../config/firebase";
export default {
  name: "add-new",
  data() {
    return {
      question: "",
      answer: ""
    };
  },
  methods: {
    addNew: function() {
      db.collection("questions").add({
        question: this.question,
        answer: this.answer
      });
    }
  }
};
</script>

<style scoped>
.login {
  margin-top: 40px;
}
input,
textarea {
  margin: 10px 0;
  width: 20%;
  padding: 15px;
  border: 1px solid #eee;
}
button {
  margin-top: 20px;
  width: 10%;
  cursor: pointer;
}
p {
  margin-top: 40px;
  font-size: 13px;
}
p a {
  text-decoration: underline;
  cursor: pointer;
}
</style>
