<template>
  <layout>
    <template>
      <h3>Log In</h3>
      <input type="text" aria-label="email" v-model="email" placeholder="Email" />
      <input type="password" aria-label="password" v-model="password" placeholder="Password" />
      <button @click="login">Log In</button>
      <p>
        You don't have an account ? You can create one
        <router-link to="/sign-up">here</router-link>.
      </p>
    </template>
  </layout>
</template>

<script>
import { auth } from "@/config/firebase";
import BaseLayout from "@/components/BaseLayout";

export default {
  name: "login",
  data() {
    return {
      email: "",
      password: ""
    };
  },
  components: {
    layout: BaseLayout
  },
  methods: {
    login: function() {
      auth.signInWithEmailAndPassword(this.email, this.password).then(
        () => {
          this.$router.replace("/");
        },
        err => {
          alert("Something went wrong:" + err.message);
        }
      );
    }
  }
};
</script>

<style scoped>
input {
  margin: 10px 0;
  width: 90%;
  max-width: 500px;
  padding: 15px;
  border: 1px solid #eee;
  border-radius: 0.5rem;
}
button {
  margin-top: 20px;
  width: 10%;
  cursor: pointer;
  min-width: 100px;
}
p {
  margin-top: 40px;
  font-size: 0.8rem;
}
</style>
