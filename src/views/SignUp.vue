<template>
  <div class="sign-up">
    <h3>Sign Up</h3>
    <input type="text" v-model="email" placeholder="Email" />
    <input type="password" v-model="password" placeholder="Password" />
    <button @click="signUp">Sign Up</button>
    <p>
      Already have an account ? You can log in
      <router-link to="/login">here</router-link>.
    </p>
  </div>
</template>

<script>
import { auth } from "@/config/firebase";
export default {
  name: "signup",
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
/* "scoped" attribute limit the CSS to this component only */
.sign-up {
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
