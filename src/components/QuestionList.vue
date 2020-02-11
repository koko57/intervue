<template>
  <div class="wrapper">
    <div class="input-wrapper">
      <form-input
        type="text"
        aria-label="Search"
        v-model="searchFilter"
        placeholder="Search question"
        class="input"
      />
      <search-icon class="icon" size="16" />
    </div>
    <ul v-if="filteredQuestions.length" class="list">
      <question
        v-for="q in filteredQuestions"
        v-bind:key="q.id"
        v-bind:question="q"
        v-on:updateQuestions="getCollection"
      />
    </ul>
    <p v-if="!filteredQuestions.length && !searchFilter" class="text">
      Add a new question
    </p>
    <p v-else class="text">No results found</p>
  </div>
</template>

<script>
import Question from "@/components/Question";
import { db } from "@/config/firebase";
import FormInput from "./FormInput";
import { SearchIcon } from "vue-feather-icons";

export default {
  name: "QuestionList",
  components: {
    FormInput,
    SearchIcon,
    question: Question
  },
  data() {
    return {
      questions: [],
      searchFilter: ""
    };
  },
  methods: {
    getCollection() {
      db.collection("questions")
        .orderBy("createdAt")
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
  computed: {
    filteredQuestions() {
      if (this.searchFilter) {
        return this.questions.filter(q => {
          return q.question
            .toLowerCase()
            .match(this.searchFilter.toLowerCase());
        });
      }
      return this.questions;
    }
  },
  created() {
    this.getCollection();
  }
};
</script>

<style scoped lang="scss">
.wrapper {
  width: 100%;
}
.input {
  width: 100%;
}
.input-wrapper {
  position: relative;
  width: 100%;
}
.list {
  list-style-type: none;
  padding: 0;
}
.icon {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
}
.text {
  margin: 2rem auto;
}
</style>
