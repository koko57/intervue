<template>
  <div class="login">
    <h3>Log In</h3>
    <input type="text" v-model="email" placeholder="Email" />
    <input type="password" v-model="password" placeholder="Password" />
    <button @click="login">Log In</button>
    <p>
      You don't have an account ? You can create one
      <router-link to="/sign-up">here</router-link>.
    </p>
  </div>
</template>

<script>
import { auth } from "@/config/firebase";
export default {
  name: "login",
  data() {
    return {
      email: "",
      password: ""
    };
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
/* "scoped" attribute limit the CSS to this component only */
.login {
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
input {
  margin: 10px 0;
  width: 20%;
  padding: 15px;
  border: 1px solid #eee;
  border-radius: 0.5rem;
}
button {
  margin-top: 20px;
  width: 10%;
  cursor: pointer;
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
