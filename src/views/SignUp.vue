<template>
  <base-layout>
    <auth-form
      v-bind:form="form"
      v-bind:errorMessage="errorMessage"
      v-on:submit="signUp"
    />
  </base-layout>
</template>

<script>
import { auth } from "@/config/firebase";
import AuthForm from "@/components/AuthForm";
import BaseLayout from "@/components/BaseLayout";

export default {
  name: "SignUp",
  components: {
    BaseLayout,
    AuthForm
  },
  data() {
    return {
      form: {
        type: "signup",
        title: "Sign Up",
        text: "Already have an account ? You can log in",
        link: "/login"
      },
      errorMessage: ""
    };
  },
  methods: {
    signUp(data) {
      auth.createUserWithEmailAndPassword(data.email, data.password).then(
        () => {
          this.$router.replace("/");
        },
        err => {
          this.errorMessage = err.message;
        }
      );
    }
  }
};
</script>
