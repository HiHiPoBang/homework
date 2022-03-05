<template>
  <div class="FoodCardGroup">
    <div
      class="FoodCardGroup__card"
      v-for="food in list"
      :key="food.ID"
    >
      <img class="FoodCardGroup__img" :src="food.PicURL" :alt="food.Name">
      <section class="FoodCardGroup__section">
        <CityLabel class="FoodCardGroup__city" :city="food.City" />
        <TownLabel class="FoodCardGroup__town" :town="food.Town" />
        <h4 class="FoodCardGroup__name">{{food.Name}}</h4>
        <p class="FoodCardGroup__feature" v-html="food.FoodFeature"></p>
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
.FoodCardGroup {
  $columnWidth: calc(50% - .5rem);
  display: grid;
  grid-template-columns: $columnWidth $columnWidth;
  column-gap: 1rem;
  row-gap: 1rem;
  @include mobile{
    grid-template-columns: 100%;
  }
  &__card {
    position: relative;
    height: 200px;
    overflow: hidden;
    transition: background-color .3s;
    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      background: linear-gradient(to bottom, rgba(0, 0, 0, 0) 0%, rgba(0, 0, 0, 0.7) 100%);
    }
    &:hover {
      &::before {
        background: transparent;
      }
      .FoodCardGroup__img {
        width: 110%;
      }
      .FoodCardGroup__feature {
        height: 40px;
        padding-top: 1rem;
        &::before {
          width: 50px;
        }
      }
    }
  }
  &__img {
    width: 100%;
    transition: width .5s;
  }
  &__section {
    position: absolute;
    left: 0;
    bottom: 0;
    box-sizing: border-box;
    width: 100%;
    padding: 1rem;
  }
  &__town {
    color: white;
  }
  &__name {
    margin: 0.5rem 0 0 0;
    color: white;
  }
  &__feature {
    position: relative;
    margin: 0;
    height: 0;
    padding: 0;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    transition: height .5s, padding-top .5s;
    color: white;
    &::before {
      content: '';
      position: absolute;
      top: 0.5rem;
      left: 0;
      width: 0;
      height: 3px;
      background-color: white;
      transition: width .3s;
    }
  }
}
</style>