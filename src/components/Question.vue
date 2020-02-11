<template>
  <div class="list-item">
    <div class="list-item--question">
      {{ question.question }}
    </div>
    <div class="list-item--level" v-if="question.level || question.category">
      <span>{{ question.level }}</span>
      <span v-if="question.level && question.category">|</span>
      <span>{{ question.category }}</span>
    </div>
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
      <x-icon size="16" />
    </button>
    <button
      class="button button__edit"
      title="Add/edit answer"
      v-on:click="edit"
    >
      <edit-icon size="16" />
    </button>
  </div>
</template>

<script>
import { db } from "@/config/firebase";
import { EditIcon, XIcon } from "vue-feather-icons";

export default {
  name: "QuestionList",
  components: {
    EditIcon,
    XIcon
  },
  data() {
    return {
      addAnswer: false,
      answer: ""
    };
  },
  props: {
    question: Object
  },
  created() {
    this.answer = this.$props.question.answer;
  },
  methods: {
    updateQuestions(docId) {
      db.collection("questions")
        .doc(docId)
        .delete()
        .then(() => this.$emit("updateQuestions"))
        .catch(err => console.log(err)); // eslint-disable-line
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
        .catch(err => console.log(err)); // eslint-disable-line
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../styles/variables";
@import "../styles/mixins";

.list-item {
  min-height: 80px;
  margin: 0.5rem 0;
  padding: 1rem;
  position: relative;
  text-align: left;
  @include flex-column;
  @include border;

  &--question {
    font-weight: bold;
    width: 90%;
    margin-bottom: 0.5rem;
  }
  &--level {
    width: 100%;
    margin: -0.25rem 0 0.5rem;
    font-size: 0.8rem;
    color: $color-grey-dark;
    span {
      margin-right: 0.35rem;
    }
  }
}
.button {
  position: absolute;
  border: none;
  right: 1rem;
  transition: 0.2s ease;
  &__delete {
    top: 0.5rem;
    &:hover {
      color: $color-pink;
    }
  }
  &__edit {
    bottom: 0.5rem;
    &:hover {
      color: $color-green-light;
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
  padding: 1rem;
  margin-right: 1.5rem;
  flex: 1;
  @include border;
}
</style>
