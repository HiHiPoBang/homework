<template>
  <div class="LoadingBlock" v-if="isLoading">
    <img src="../assets/bars.svg" width="50px"/>
    <p class="LoadingBlock__desp">資料下載中，請稍等！</p>
  </div>
</template>

<script>
export default {
  props: {
    isLoading: {
      type: Boolean,
      default: false
    }
  },
}
</script>

<style lang="scss" scoped>
.LoadingBlock {
  z-index: 1;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, .7);
  &__desp {
    color: white;
  }
}
</style>