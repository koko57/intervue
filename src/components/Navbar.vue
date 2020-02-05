<template>
  <div class="navbar">
    <router-link to="/">Home</router-link> |
    <router-link to="/add-new">Add New</router-link> |
    <a v-on:click="logout">Log out</a>
  </div>
</template>
<script>
import { auth } from "@/config/firebase";
export default {
  name: "Navbar",
  methods: {
    logout() {
      auth.signOut().then(() => {
        this.$router.push("/login");
      });
    }
  }
};
</script>
<style lang="scss" scoped>
.navbar {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  background: white;
  a {
    display: inline-block;
    font-weight: bold;
    color: #2c3e50;
    text-decoration: none;
    padding: 1rem;
    cursor: pointer;

    &.router-link-exact-active {
      color: #42b983;
      pointer-events: none;
    }
  }
}
</style>
