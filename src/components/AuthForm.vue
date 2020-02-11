<template>
  <form>
    <h3>{{ form.title }}</h3>
    <form-input
      type="text"
      aria-label="email"
      v-model="email"
      placeholder="Email"
    />
    <span v-if="errors.email">{{ errors.email }}</span>
    <form-input
      type="password"
      aria-label="password"
      v-model="password"
      placeholder="Password"
    />
    <span v-if="errors.password">{{ errors.password }}</span>
    <form-input
      v-if="form.type === 'signup'"
      type="password"
      aria-label="confirm password"
      v-model="confirmPassword"
      placeholder="Confirm Password"
    />
    <span v-if="errors.confirmPassword">{{ errors.confirmPassword }}</span>
    <button @click="submit">{{ form.title }}</button>
    <span v-if="errorMessage">{{ errorMessage }}</span>
    <p>
      {{ form.text }}
      <router-link v-bind:to="form.link">here</router-link>.
    </p>
  </form>
</template>

<script>
import FormInput from "./FormInput";

export default {
  name: "AuthForm",
  components: {
    FormInput
  },
  data() {
    return {
      email: "",
      password: "",
      confirmPassword: "",
      errors: {
        email: "",
        password: "",
        confirmPassword: ""
      }
    };
  },
  props: {
    errorMessage: String,
    form: Object
  },
  methods: {
    submit() {
      const valid = this.validate();
      if (valid) {
        const data = {
          email: this.email,
          password: this.password
        };
        this.$emit("submit", data);
      }
    },
    validate() {
      this.clearErrors();
      if (!this.email) {
        this.errors.email = "Email is required";
      }
      if (this.email && !this.matchEmailPattern(this.email)) {
        this.errors.email = "Email is invalid";
      }
      if (!this.password) {
        this.errors.password = "Password is required";
      }
      if (
        this.$props.form.type === "signup" &&
        this.password !== this.confirmPassword
      ) {
        this.errors.confirmPassword = "Passwords are not matching";
      }
      return !Object.values(this.errors).find(error => error);
    },
    matchEmailPattern(email) {
      const re = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/i;
      return re.test(email);
    },
    clearErrors() {
      this.errors.email = "";
      this.errors.password = "";
      this.errors.confirmPassword = "";
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/variables";

form {
  width: 100%;
}
button {
  margin: 20px auto;
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
span {
  display: block;
  color: $color-pink;
  font-size: 0.9rem;
}
</style>
