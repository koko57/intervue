<template>
  <layout>
    <template>
      <h3>Sign Up</h3>
      <form-input
        type="text"
        aria-label="email"
        v-model="email"
        placeholder="Email"
      />
      <form-input
        type="password"
        aria-label="password"
        v-model="password"
        placeholder="Password"
      />
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
import FormInput from "../components/FormInput";
export default {
  name: "signup",
  components: {
    FormInput,
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
