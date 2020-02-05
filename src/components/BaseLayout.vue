<template>
  <div class="container">
    <navbar v-if="showNavbar" />
    <div class="main-wrapper">
      <slot />
    </div>
  </div>
</template>

<script>
import Navbar from "./Navbar";
export default {
  name: "BaseLayout",
  components: {
    navbar: Navbar
  },
  props: {
    showNavbar: Boolean
  }
};
</script>

<style lang="scss">
.container {
  width: 100%;
  min-height: 100vh;
}
.main-wrapper {
  width: 90%;
  max-width: 800px;
  margin: 90px auto 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}
button {
  appearance: none;
  padding: 0.25rem 0.5rem;
  border: 1px solid #eee;
  border-radius: 0.5rem;
  cursor: pointer;
  &:hover {
    border-color: #777;
  }
}
</style>
