<template>
  <div class="FoodList">
    <div
      class="FoodList__row"
      v-for="food in list"
      :key="food.ID"
    >
      <div class="FoodList__thumbnail"><img :src="food.PicURL" :alt="food.Name"></div>
      <section class="FoodList__section">
        <h1 class="FoodList__name">{{food.Name}}</h1>
        <CityLabel class="FoodList__city" :city="food.City" />
        <TownLabel class="FoodList__town" :town="food.Town" />
        <p class="FoodList__feature" v-html="food.FoodFeature"></p>
      </section>
    </div>
  </div>
</template>

<script>
import CityLabel from './CityLabel.vue';
import TownLabel from './TownLabel.vue';
export default {
  components: {
    CityLabel,
    TownLabel
  },
  props: {
    list: {
      type: Array,
      default: () => ([])
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/rwd.scss';
.FoodList {
  padding-left: 100px;
  text-align: left;
  @include mobile{
    padding: 0px 1rem;
  }
  &__row {
    position: relative;
    display: flex;
    align-items: flex-start;
    margin-bottom: 1rem;
    padding: 1rem;
    background-color: white;
    @include mobile{
      flex-direction: column;
    }
  }
  &__thumbnail {
    margin: 0;
    min-width: 200px;
    max-width: 200px;
    height: auto;
    img {
      width: 100%;
      height: auto;
    }
    @include mobile{
      min-width: 100%;
      max-width: 100%;
    }
  }
  &__section {
    flex-grow: 1;
    padding-left: 1rem;
    @include mobile{
      padding-left: 0;
    }
  }
  &__city {
    position: absolute;
    top: 0;
    left: -64px;
    @include mobile{
      position: static;
    }
  }
  &__town {
    position: absolute;
    top: 35px;
    left: -35px;
    width: 20px;
    @include mobile{
      position: static;
      width: auto;
    }
  }
  &__name {
    @include mobile {
      margin-top: 1rem;
    }
  }
  &__feature {
    height: 70px;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    @include mobile{
      margin: 1rem 0 0 0;
      height: 45px;
      -webkit-line-clamp: 2;
    }
  }
}
</style>