<template>
  <div class="FoodIntroduction">
    <div class="FoodIntroduction__featureBar">
      <div class="FoodIntroduction__selectGroup">
        <base-select
          class="FoodIntroduction__select"
          :options="cityOptions"
          placeholder="請選擇行政區域..."
          @change="cityChangeHandler"
        />
        <base-select
          class="FoodIntroduction__select"
          :options="townOptions"
          placeholder="請選擇鄉鎮區域..."
          @change="currentTown = $event"
        />
      </div>
      <div class="FoodIntroduction__modeTypes">
        <label class="FoodIntroduction__modeLabel">檢視模式</label>
        <button
          class="FoodIntroduction__modeButton"
          :class="{'FoodIntroduction__modeButton--active': mode === MODE_TYPE_MAP.list}"
          @click="changeMode(MODE_TYPE_MAP.list)">
          <font-awesome-icon icon="fa-solid fa-list" />
        </button>
        <button
          class="FoodIntroduction__modeButton"
          :class="{'FoodIntroduction__modeButton--active': mode === MODE_TYPE_MAP.table}"
          @click="changeMode(MODE_TYPE_MAP.table)"
        >
          <font-awesome-icon icon="fa-solid fa-bars" />
        </button>
        <button
          class="FoodIntroduction__modeButton"
          :class="{'FoodIntroduction__modeButton--active': mode === MODE_TYPE_MAP.card}"
          @click="changeMode(MODE_TYPE_MAP.card)"
        >
          <font-awesome-icon icon="fa-solid fa-table-cells-large" />
        </button>
      </div>
    </div>
    <div class="FoodIntroduction__introContainter">
      <food-list
        class="FoodIntroduction__intro FoodIntroduction__intro--list"
        v-if="mode === MODE_TYPE_MAP.list"
        :list="listForRender"
      />
      <food-table
        class="FoodIntroduction__intro FoodIntroduction__intro--table"
        v-else-if="mode === MODE_TYPE_MAP.table"
        :list="listForRender"
      />
      <food-card-group
        class="FoodIntroduction__intro FoodIntroduction__intro--card"
        v-else
        :list="listForRender"
      />
    </div>
    <base-pagination
      class="FoodIntroduction__basePagination"
      :size="pageSize"
      :total="listAfterFilter.length"
      :currentPage="currentPage"
      @change-page="currentPage = $event.page"
    />
    <loading-block :isLoading="isLoading" />
  </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faList, faBars, faTableCellsLarge } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import BaseSelect from './BaseSelect.vue';
import FoodList from './FoodList.vue';
import FoodTable from './FoodTable.vue';
import FoodCardGroup from './FoodCardGroup.vue'
import BasePagination from './BasePagination.vue';
import LoadingBlock from './LoadingBlock.vue';

library.add(faList, faBars, faTableCellsLarge);
const MODE_TYPE_MAP = {
  list: 'list',
  table: 'table',
  card: 'card',
}
export default {
  components: {
    FontAwesomeIcon,
    BaseSelect,
    FoodList,
    FoodTable,
    FoodCardGroup,
    BasePagination,
    LoadingBlock
  },
  data () {
    return {
      MODE_TYPE_MAP,
      mode: MODE_TYPE_MAP.table,
      list: [],
      currentCity: null,
      currentTown: null,
      currentPage: 1,
      pageSize: 10,
      isLoading: false,
    }
  },
  computed: {
    cityOptions() {
      return this.list.reduce((acm, food) => {
        const matchCityIndex = acm.findIndex(({ value }) => value === food.City);
        if (matchCityIndex === -1) {
          acm.push({
            value: food.City,
            text: food.City,
            towns: [{ value: food.Town, text: food.Town}]
          })
        } else {
          const isTownExisted = acm[matchCityIndex].towns.findIndex(({ value }) => value === food.Town) !== -1;
          if (!isTownExisted) acm[matchCityIndex].towns.push({
            value: food.Town,
            text: food.Town,
          });
        }
        return acm;
      }, []);
    },
    townOptions() {
      const result = this.cityOptions.find(({ value }) => value === this.currentCity);
      return result?.towns || [];
    },
    listAfterFilter() {
      const isCityMatch = (city) => (city === this.currentCity);
      const isTownMatch = (town) => (this.currentTown ? town === this.currentTown : true);
      const matchSelectsValue = ({City, Town}) => (isCityMatch(City) && isTownMatch(Town));
      return this.currentCity
        ? this.list.filter(matchSelectsValue)
        : this.list
    },
    listForRender() {
      const addNewAttribute = (food, index) => ({...food, No: index + 1});
      
      const startPage = (this.currentPage - 1) * this.pageSize;
      const endPage = startPage + this.pageSize;
      const filterByPagination = (__, index) => (index >= startPage && index < endPage);

      return this.listAfterFilter
        .map(addNewAttribute)
        .filter(filterByPagination);
    }
  },
  methods: {
    changeMode(mode = '') {
      this.mode = mode;
    },
    cityChangeHandler(val = '') {
      this.currentCity = val;
      this.currentTown = null;
    },
    fetchList() {
      return fetch('https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx')
        .then((response) => {
          return response.json();
        })
        .catch((err) => {
          throw new Error(err);
        })
    },
  },
  async created() {
    this.isLoading = true;
    this.list = await this.fetchList();
    this.isLoading = false;
  }
}
</script>

<style lang="scss" scoped>
@import '../style/rwd.scss';
.FoodIntroduction {
  box-sizing: border-box;
  width: 70vw;
  padding: 0 1rem;
  @include mobile {
    width: 100vw;
    max-width: 100vw;
  }
  &__featureBar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
    @include mobile {
      flex-direction: column;
    }
  }
  &__selectGroup {
    @include mobile {
      display: flex;
      flex-direction: column;
    }
  }
  &__select {
    margin-right: 1rem;
    @include mobile {
      margin-right: 0;
      margin-bottom: 1rem;
    }
  }
  &__modeTypes {
    @include mobile {
      display: flex;
      justify-content: center;
    }
  }
  &__modeLabel {
    color: #919594;
  }
  &__modeButton {
    margin-left: 1rem;
    outline: 0;
    border-width: 0;
    background: 0;
    font-size: 1rem;
    color: #666666;
    &--active {
      color: black;
    }
  }
  &__introContainter {
    @include mobile {
      max-width: 100%;
      overflow: auto;
    }
    
  }
  &__basePagination {
    margin-top: 1rem;
  }
}
</style>