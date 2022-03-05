<template>
  <label class="TownLabel">{{ town }}</label>
</template>

<script>
export default {
  props: {
    town: {
      type: String
    },
  }
}
</script>

<style lang="scss" scoped>
.TownLabel {
  padding: 0.125rem 0.5rem;
  font-size: 0.875rem;
  color: #666666;
}
</style>