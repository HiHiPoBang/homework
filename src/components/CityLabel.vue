<template>
  <label class="CityLabel">{{ city }}</label>
</template>

<script>
export default {
  props: {
    city: {
      type: String,
    }
  }
}
</script>

<style lang="scss" scoped>
.CityLabel {
  padding: 0.125rem 0.5rem;
  background-color: #0ca2d4;
  font-size: 0.875rem;
  color: white;
}
</style>