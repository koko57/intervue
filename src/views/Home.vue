<template>
  <base-layout v-bind:showNavbar="true">
    <template>
      <question-list />
    </template>
  </base-layout>
</template>

<script>
import QuestionList from "@/components/QuestionList.vue";
import BaseLayout from "@/components/BaseLayout";

export default {
  name: "Home",
  components: {
    QuestionList,
    BaseLayout
  }
};
</script>
