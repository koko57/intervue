<template>
  <base-layout>
    <auth-form
      v-bind:form="form"
      v-bind:errorMessage="errorMessage"
      v-on:submit="login"
    />
  </base-layout>
</template>

<script>
import { auth } from "@/config/firebase";
import BaseLayout from "@/components/BaseLayout";
import AuthForm from "@/components/AuthForm";

export default {
  name: "login",
  data() {
    return {
      form: {
        type: "login",
        title: "Log In",
        text: "You don't have an account ? You can create one",
        link: "/sign-up"
      },
      errorMessage: ""
    };
  },
  components: {
    AuthForm,
    BaseLayout
  },
  methods: {
    login(data) {
      auth.signInWithEmailAndPassword(data.email, data.password).then(
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
