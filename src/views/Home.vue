<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div v-for="q in questions" v-bind:key="q.id">
      <div>{{ q.question }}</div>
      <div>{{ q.answer }}</div>
      <div>{{ q.addedBy }}</div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import { db } from "@/config/firebase";
export default {
  name: "home",
  components: {
    HelloWorld
  },
  data() {
    return {
      questions: []
    };
  },
  created() {
    db.collection("questions")
      .get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          const qa = { id: doc.id, ...doc.data() };
          this.questions.push(qa);
        });
      });
  }
};
</script>
