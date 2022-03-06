<template>
  <div id="app" class="App">
    <header><h1 class="App__title">農村地方美食小吃特色料理</h1></header>
    <main class="App__main">
      <food-introduction class="App__foodIntroduction"/>
      <advertisement-block class="App__advertisementBlock"/>
    </main>
    <BaseFooter class="App__footer"/>
  </div>
</template>

<script>
import FoodIntroduction from './components/FoodIntroduction.vue';
import AdvertisementBlock from './components/AdvertisementBlock.vue'
import BaseFooter from './components/BaseFooter.vue'
export default {
  name: 'App',
  components: {
    FoodIntroduction,
    AdvertisementBlock,
    BaseFooter
  }
}
</script>

<style lang="scss">
@import './style/rwd.scss';
body {
  margin: 0;
}
h1 {
  margin: 0;
  margin-bottom: 1rem;
  font-size: 1.5rem;
}
p {
  font-size: 0.875rem;
  color: #666666;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.App {
  min-width: 100vw;
  min-height: 100vh;
  padding-bottom: 100px;
  background-color: #eeeeee;
  &__main {
    display: flex;
  }
  &__title {
    padding: 2rem 1rem 0 1rem;
    text-align: center;
  }
  &__advertisementBlock{
    flex-grow: 1;
    @include mobile{
      display: none;
    }
  }
  &__footer {
    position: fixed;
    left: 0;
    bottom: 0;
    box-sizing: border-box;
    width: 100%;
  }
}
</style>