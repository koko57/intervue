<template>
  <input
    v-bind:value="value"
    v-on:input="$emit('input', $event.target.value)"
  />
</template>

<script>
export default {
  name: "FormInput",
  props: ["value"]
};
</script>

<style lang="scss" scoped>
@import "../styles/variables";
@import "../styles/mixins";

input {
  margin: 10px auto;
  width: 90%;
  padding: 1rem;
  @include border;
}
</style>
