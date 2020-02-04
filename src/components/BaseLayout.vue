<template>
  <div class="container">
    <navbar />
    <div class="main-wrapper">
      <slot name="main" />
    </div>
  </div>
</template>

<script>
import Navbar from "./Navbar";
export default {
  name: "BaseLayout",
  components: {
    navbar: Navbar
  }
};
</script>

<style lang="scss">
.container {
  width: 90%;
  max-width: 800px;
  margin: 0 auto;
}
.main-wrapper {
  margin-top: 90px;
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
