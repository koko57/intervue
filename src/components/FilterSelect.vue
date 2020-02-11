<template>
  <div class="select-wrapper">
    <div class="select-wrapper__inner">
      <select v-model="value.level" aria-label="level">
        <option value="">Level</option>
        <option>Junior</option>
        <option>Mid</option>
        <option>Senior</option>
      </select>
      <chevron-down-icon class="icon" size="16" />
    </div>
    <div class="select-wrapper__inner">
      <select v-model="value.category" aria-label="category">
        <option value="">Category</option>
        <option>JavaScript</option>
        <option>CSS</option>
        <option>HTML</option>
        <option>General</option>
      </select>
      <chevron-down-icon class="icon" size="16" />
    </div>
  </div>
</template>

<script>
import { ChevronDownIcon } from "vue-feather-icons";
export default {
  name: "FilterSelect",
  components: {
    ChevronDownIcon
  },
  props: {
    value: Object
  }
};
</script>

<style scoped lang="scss">
@import "../styles/variables";
@import "../styles/mixins";

.select-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  &__inner {
    position: relative;
  }
}
.icon {
  position: absolute;
  top: 2rem;
  right: 2rem;
}
select {
  appearance: none;
  min-width: 200px;
  padding: 1rem;
  margin: 1rem;
  background: none;
  display: inline-block;
  @include border;
}
</style>
