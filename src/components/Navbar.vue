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
@import "../styles/variables";

.navbar {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  background: white;
  a {
    display: inline-block;
    padding: 1rem;
    color: $color-green-dark;
    font-weight: bold;
    text-decoration: none;
    cursor: pointer;

    &.router-link-exact-active {
      color: $color-green-light;
      pointer-events: none;
    }
  }
}
</style>
