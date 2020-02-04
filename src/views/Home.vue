<template>
  <layout>
    <template v-slot:main>
      <question-list />
    </template>
  </layout>
</template>

<script>
import QuestionList from "@/components/QuestionList.vue";
import BaseLayout from "@/components/BaseLayout";

export default {
  name: "home",
  components: {
    "question-list": QuestionList,
    layout: BaseLayout
  },
};
</script>
