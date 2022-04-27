<template>
  <div class="container">
    <slot />
  </div>
</template>

<script>
export default {
  name: "BaseContainer",
};
</script>

<style lang="scss">
.container {
  width: 100%;
  max-width: 1140px;
  margin: 0 auto;
  padding: 0 15px;
}
</style>
