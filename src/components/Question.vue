<template>
  <div class="list-item">
    <div class="list-item--question">{{ question.question }}</div>
    <div>{{ question.answer }}</div>
    <div v-if="addAnswer" class="textarea-wrapper">
      <textarea aria-label="answer" v-model="answer" />
      <button type="button" v-on:click="editAnswer(question.id)">Submit</button>
    </div>
    <button
      class="button button__delete"
      title="Delete question"
      v-on:click="updateQuestions(question.id)"
    >
      x
    </button>
    <button
      class="button button__edit"
      title="Add/edit answer"
      v-on:click="edit"
    >
      edit
    </button>
  </div>
</template>

<script>
import { db } from "@/config/firebase";
export default {
  name: "QuestionList",
  data() {
    return {
      addAnswer: false,
      answer: ""
    };
  },
  methods: {
    updateQuestions(docId) {
      db.collection("questions")
        .doc(docId)
        .delete()
        .then(() => this.$emit("updateQuestions"))
        .catch(err => console.log(err));
    },
    edit() {
      this.addAnswer = !this.addAnswer;
    },
    editAnswer(docId) {
      db.collection("questions")
        .doc(docId)
        .update({
          answer: this.answer
        })
        .then(() => {
          this.$emit("updateQuestions");
          this.addAnswer = false;
        })
        .catch(err => console.log(err));
    }
  },
  created() {
    this.answer = this.$props.question.answer;
  },
  props: {
    question: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.list-item {
  min-height: 80px;
  margin: 0.5rem 0;
  display: flex;
  flex-direction: column;
  position: relative;
  text-align: left;
  padding: 1rem;
  border: 1px solid #eee;
  border-radius: 1rem;
  &--question {
    font-weight: bold;
  }
}
.button {
  position: absolute;
  right: 1rem;
  transition: 0.2s ease;
  &__delete {
    top: 0.5rem;
    &:hover {
      border-color: #cd6183;
    }
  }
  &__edit {
    bottom: 0.5rem;
    &:hover {
      border-color: #42b983;
    }
  }
}
.textarea-wrapper {
  margin: 10px 0;
  width: 90%;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}
textarea {
  padding: 15px;
  border: 1px solid #eee;
  border-radius: 0.5rem;
  flex: 1;
  margin-right: 1.5rem;
}
</style>
