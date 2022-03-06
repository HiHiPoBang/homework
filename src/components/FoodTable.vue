<template>
  <table class="FoodTable">
    <thead class="FoodTable__header">
      <tr class="FoodTable__row">
        <th class="FoodTable__col FoodTable__col--no">編號</th>
        <th class="FoodTable__col FoodTable__col--city">行政區域</th>
        <th class="FoodTable__col FoodTable__col--town">鄉鎮區</th>
        <th class="FoodTable__col FoodTable__col--name">商家</th>
        <th class="FoodTable__col FoodTable__col--address">地址</th>
      </tr>
    </thead>
    <tbody class="FoodTable__body">
      <tr
        class="FoodTable__row"
        v-for="food in list"
        :key="food.ID"
      >
        <th class="FoodTable__col FoodTable__col--no">{{ food.No }}</th>
        <th class="FoodTable__col FoodTable__col--city">{{ food.City }}</th>
        <th class="FoodTable__col FoodTable__col--town">{{ food.Town }}</th>
        <th class="FoodTable__col FoodTable__col--name">{{ food.Name }}</th>
        <th class="FoodTable__col FoodTable__col--address" :data-content="food.Address">
          <span>{{food.Address}}</span>
        </th>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      default: () => ([])
    }
  }
}
</script>

<style lang="scss" scoped>
table, th, td {
  border: 1px solid #dddddd;
  border-collapse: collapse;
}
.FoodTable {
  width: auto;
  min-width: 100%;
  &__row {
    width: 100%;
    background-color: white;
    &:nth-child(even) {
      background-color: #f9f9f9;
    }
  }
  &__header &__row {
    background-color: #f1f1f1;
  }
  &__body &__row {
    &:hover {
      background-color: #eff4f7;
    }
  }
  &__col {
    padding: 1rem;
    text-align: left;
    font-weight: normal;
    white-space: nowrap;
    &--no {
      width: 8%;
      text-align: right;
    }
    &--city, &--town {
      width: 10%
    }
    &--name {
      width: 20%;
    }
    &--address {
      position: relative;
      max-width: 200px;
      span {
        display: inline-block;
        max-width: 100%;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
      }
      &:hover {
        &::before {
          content: attr(data-content);
          position: absolute;
          bottom: -20px;
          left: 30px;
          border: 1px solid #ddd;
          padding: .5rem;
          background-color: white;
        }
      }
    }
  }
  &__header &__col {
    text-align: center;
  }
}
</style>