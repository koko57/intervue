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
      <search-icon class="icon__search" size="16" />
    </div>
    <div
      class="wrapper wrapper--filter wrapper--filter__main"
      v-if="questions.length"
    >
      <div
        class="wrapper--filter wrapper--filter__title"
        v-on:click="toggleFilters"
        role="button"
      >
        <p>Filter by:</p>
        <chevron-down-icon
          v-bind:class="addFilters && 'rotate'"
          class="icon"
          size="16"
        />
      </div>
      <filter-select v-model="filters" v-if="addFilters" />
      <div
        class="wrapper--filter wrapper--filter__title"
        v-if="addFilters"
        v-on:click="clearFilters"
        role="button"
      >
        Clear Filters
        <x-icon class="icon icon__x" size="16" />
      </div>
    </div>
    <ul v-if="filteredQuestions.length" class="list">
      <question
        v-for="q in filteredQuestions"
        v-bind:key="q.id"
        v-bind:question="q"
        v-on:updateQuestions="getCollection"
      />
    </ul>
    <div v-if="!filteredQuestions.length">
      <p v-if="!searchFilter && !addFilters" class="text">
        Add a new question
      </p>
      <p v-else class="text">No results found</p>
    </div>
  </div>
</template>

<script>
import Question from "@/components/Question";
import { db } from "@/config/firebase";
import FormInput from "./FormInput";
import FilterSelect from "./FilterSelect";
import { SearchIcon, ChevronDownIcon, XIcon } from "vue-feather-icons";

export default {
  name: "QuestionList",
  components: {
    FilterSelect,
    FormInput,
    SearchIcon,
    ChevronDownIcon,
    XIcon,
    question: Question
  },
  data() {
    return {
      questions: [],
      searchFilter: "",
      filters: { level: "", category: "" },
      addFilters: false
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
    },
    clearFilters() {
      this.filters = {
        level: "",
        category: ""
      };
    },
    toggleFilters() {
      if (this.addFilters) {
        this.clearFilters();
      }
      this.addFilters = !this.addFilters;
    }
  },
  computed: {
    filteredQuestions() {
      let questions = this.questions;
      if (this.filters.level) {
        questions = questions.filter(q => {
          return q.level === this.filters.level;
        });
      }
      if (this.filters.category) {
        questions = questions.filter(q => {
          return q.category === this.filters.category;
        });
      }
      if (this.searchFilter) {
        questions = questions.filter(q => {
          return q.question
            .toLowerCase()
            .match(this.searchFilter.toLowerCase());
        });
      }
      return questions;
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
  &--filter {
    display: flex;
    &__main {
      justify-content: space-between;
    }
    &__title {
      padding: 1rem;
      cursor: pointer;
      &:hover .icon__x {
        color: #cd6183;
      }
    }
  }
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
  margin: 0.25rem 0.5rem;
  transition: 0.3s ease;
  &__search {
    position: absolute;
    top: 1.5rem;
    right: 1.5rem;
  }
}
.text {
  margin: 2rem auto;
}
.rotate {
  transform: rotate(180deg);
}
</style>
