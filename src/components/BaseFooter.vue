<template>
  <footer class="BaseFooter">
    <h3 class="BaseFooter__infoLabel">CMoney 全曜財經資訊</h3>
    <h4 class="BaseFooter__infoLabel">
      <span>資訊來源: </span>
      <span class="BaseFooter__sourceLabel">政府資料開放平臺</span>
    </h4>
  </footer>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.BaseFooter {
  padding: 1rem;
  background-color: #999999;
  text-align: center;
  color: #b5bec3;
  &__infoLabel {
    margin: 0;
  }
  &__sourceLabel {
    color: white;
  }
}
</style>