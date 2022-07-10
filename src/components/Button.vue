<template>
  <button class="btn" @click="$emit('click')">
    <slot />
  </button>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.btn {
  position: relative;
  width: calc(20% - 4px);
  border: 1px solid black;
  margin: 2px;
  font-size: 24px;
  border-radius: 5px;
  color: #bab6d4;
  background-color: #3f3f42;
  transition: all linear 0.1s;
  &:hover {
    color: #000000;
    background-color: #bab6d4;
  }
  &:active {
    background-color: #9794a9;
  }
}
</style>