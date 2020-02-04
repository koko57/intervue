<template>
  <div class="hello">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/add-new">Add New</router-link> |
      <span v-on:click="logout">Log out</span>
    </div>
  </div>
</template>

<script>
import { auth } from "@/config/firebase";
export default {
  name: "HelloWorld",
  methods: {
    logout() {
      auth.signOut().then(() => {
        this.$router.push("/login");
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
button {
  appearance: none;
}
</style>
