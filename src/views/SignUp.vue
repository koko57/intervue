<template>
  <layout>
    <template>
      <h3>Sign Up</h3>
      <input type="text" aria-label="email" v-model="email" placeholder="Email" />
      <input type="password" aria-label="password" v-model="password" placeholder="Password" />
      <button @click="signUp">Sign Up</button>
      <p>
        Already have an account ? You can log in
        <router-link to="/login">here</router-link>.
      </p>
    </template>
  </layout>
</template>

<script>
import { auth } from "@/config/firebase";
import BaseLayout from "../components/BaseLayout";
export default {
  name: "signup",
  components: {
    layout: BaseLayout
  },
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    signUp: function() {
      auth.createUserWithEmailAndPassword(this.email, this.password).then(
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
  font-size: 13px;
}
p a {
  text-decoration: underline;
  cursor: pointer;
}
</style>
