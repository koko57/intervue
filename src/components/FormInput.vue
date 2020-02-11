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

<style scoped>
input {
  margin: 10px auto;
  width: 90%;
  padding: 1rem;
  border: 1px solid #eee;
  border-radius: 0.5rem;
}
</style>
