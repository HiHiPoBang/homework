<template>
  <div class="AdvertisementBlock">
    <img class="AdvertisementBlock__adImg" src="../assets/adv1.png" />
    <img class="AdvertisementBlock__adImg" src="../assets/adv2.png" />
    <img class="AdvertisementBlock__adImg AdvertisementBlock__adImg--final" src="../assets/adv3.png" />
  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss" scoped>
.AdvertisementBlock {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  &__adImg {
    margin-bottom: 1rem;
    &--final {
      position: -webkit-sticky;
      position: sticky;
      top: 1rem;
    }
  }
}
</style>