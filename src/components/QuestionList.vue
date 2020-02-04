<template>
  <ul class="list">
    <question
      v-for="q in questions"
      v-bind:key="q.id"
      v-bind:question="q"
      v-on:updateQuestions="getCollection"
    />
  </ul>
</template>

<script>
import Question from "@/components/Question";
import { db } from "@/config/firebase";

export default {
  name: "QuestionList",
  components: {
    question: Question
  },
  data() {
    return {
      questions: []
    };
  },
  methods: {
    getCollection() {
      db.collection("questions")
        .get()
        .then(querySnapshot => {
          const questions = [];
          querySnapshot.forEach(doc => {
            const qa = { id: doc.id, ...doc.data() };
            questions.push(qa);
          });
          this.questions = questions;
        });
    }
  },
  created() {
    this.getCollection();
  }
};
</script>

<style scoped lang="scss">
.list {
  list-style-type: none;
  padding: 0;
}
</style>
