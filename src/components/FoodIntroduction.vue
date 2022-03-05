<template>
  <div class="FoodIntroduction">
    <div class="FoodIntroduction__featureBar">
      <div class="FoodIntroduction__selectGroup">
        <base-select class="FoodIntroduction__select" placeholder="請選擇行政區域..." />
        <base-select class="FoodIntroduction__select" placeholder="請選擇鄉鎮區域..." />
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
        :list="list"
      />
      <food-table
        class="FoodIntroduction__intro FoodIntroduction__intro--table"
        v-else-if="mode === MODE_TYPE_MAP.table"
        :list="list"
      />
      <food-card-group
        class="FoodIntroduction__intro FoodIntroduction__intro--card"
        v-else
        :list="list"
      />
    </div>
    <base-pagination class="FoodIntroduction__basePagination"/>
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
  },
  data () {
    return {
      MODE_TYPE_MAP,
      mode: MODE_TYPE_MAP.table,
      list: [
        {
          "ID": "01_102",
          "Name": "甘露自然蔬食餐廳",
          "Address": "苗栗縣三義鄉廣盛村中正路 80號 /苗栗縣通霄鎮楓樹里楓樹窩92-2號",
          "Tel": "037-877546 ",
          "HostWords": "甘露一直以來推動的自然飲食，即是一種尊重大自然、順應大地、感恩惜福的飲食文化，在每一道餐點中，開創出一條與萬物共生共榮之路。甘露順應季節、以當季、當地的有機食材為主軸，開發具地方特色的有機蔬食料理，真正讓消費者能感受從產地到餐桌的米淇林饗宴。餐點所使用的調味料以本土在地油品及傳統天然手作醬油、糙米醋為主，堅持不添加任何化學添加物，讓消費者不用擔心食安的問題；而烹調方式強調低碳節能的環保概念，不高溫油炸，以生食、涼拌、蒸、燙為主，更保留食物的風味與營養，照顧用餐者的健康。更期望用敬天愛地、感恩惜福的態度，提供大家一種更友善的飲食方式，為後代子孫及萬物生靈預約一個和諧互助與真善美的未來！<br><br>\r\n\r\n招牌菜：塔香豆腐<br>\r\n招牌菜介紹：以有機黃豆搭配深海鹽滷，手工製作的新鮮豆腐，搭配農場種植的有機九層塔，塔香與豆香味的結合，吃起來清爽、美味，相當受歡迎。 ",
          "Price": "",
          "OpenHours": "",
          "CreditCard": "False",
          "TravelCard": "False",
          "TrafficGuidelines": "",
          "ParkingLot": "",
          "Url": "",
          "Email": "",
          "BlogUrl": "",
          "PetNotice": "",
          "Reminder": "",
          "FoodMonths": "",
          "FoodCapacity": "",
          "FoodFeature": "甘露一直以來推動的自然飲食，即是一種尊重大自然、順應大地、感恩惜福的飲食文化，在每一道餐點中，開創出一條與萬物共生共榮之路。甘露順應季節、以當季、當地的有機食材為主軸，開發具地方特色的有機蔬食料理，真正讓消費者能感受從產地到餐桌的米淇林饗宴。餐點所使用的調味料以本土在地油品及傳統天然手作醬油、糙米醋為主，堅持不添加任何化學添加物，讓消費者不用擔心食安的問題；而烹調方式強調低碳節能的環保概念，不高溫油炸，以生食、涼拌、蒸、燙為主，更保留食物的風味與營養，照顧用餐者的健康。更期望用敬天愛地、感恩惜福的態度，提供大家一種更友善的飲食方式，為後代子孫及萬物生靈預約一個和諧互助與真善美的未來！<br><br>\r\n\r\n招牌菜：塔香豆腐<br>\r\n招牌菜介紹：以有機黃豆搭配深海鹽滷，手工製作的新鮮豆腐，搭配農場種植的有機九層塔，塔香與豆香味的結合，吃起來清爽、美味，相當受歡迎。 ",
          "City": "苗栗縣",
          "Town": "三義鄉",
          "Coordinate": "24.4146177,120.772363",
          "PicURL": "https://ezgo.coa.gov.tw/Uploads/opendata/TainmaMain01/APPLY_D/20151007173235.jpg"
        },
        {
          "ID": "01_103",
          "Name": "卓也小屋田媽媽",
          "Address": "苗栗縣三義鄉雙潭村崩山下 1-9 號",
          "Tel": "(037) 879-198",
          "HostWords": "中國在三千多年前已經知道利用生鮮藍草染色。我們耳熟能詳的「青出於藍」這句古老諺語，便是出自荀子，由於目睹染匠從綠色「藍草」中染出更為出色的青豔色彩，因此從不可思議的轉化過程與其染色結果，因而發出「青取之於藍，而青於藍」的喟嘆。其實現在有許多植物含有許多天然色素可供染色，甚至可用來入菜，讓餐點能夠以更健康的方式呈現豐富的色彩。<br><br>\r\n\r\n名鋤擺桌現在走向以「食農教育-染人體驗」為發展方向，透過簡報檔進行解說，以及實地到訪染料植物園進行田園染料植物巡禮，讓大家學習、認識可用來染色之植物，並因應時節進行簡單之農事操作或收割，再來將染料植物或食材進行調製、加工處理，並將染料植物入菜烹調，讓遊客自己體驗如何將染料植物入菜，烹調完成後便可自行享用自己烹調之菜色，用完餐後可至染工坊實際體驗天然植物染布過程，集學習、體驗、娛樂於一體。此外，在這裡也有許多精緻植物染精品可供挑選。",
          "Price": "",
          "OpenHours": "",
          "CreditCard": "False",
          "TravelCard": "False",
          "TrafficGuidelines": "",
          "ParkingLot": "",
          "Url": "",
          "Email": "",
          "BlogUrl": "",
          "PetNotice": "",
          "Reminder": "",
          "FoodMonths": "",
          "FoodCapacity": "",
          "FoodFeature": "中國在三千多年前已經知道利用生鮮藍草染色。我們耳熟能詳的「青出於藍」這句古老諺語，便是出自荀子，由於目睹染匠從綠色「藍草」中染出更為出色的青豔色彩，因此從不可思議的轉化過程與其染色結果，因而發出「青取之於藍，而青於藍」的喟嘆。其實現在有許多植物含有許多天然色素可供染色，甚至可用來入菜，讓餐點能夠以更健康的方式呈現豐富的色彩。<br><br>\r\n\r\n名鋤擺桌現在走向以「食農教育-染人體驗」為發展方向，透過簡報檔進行解說，以及實地到訪染料植物園進行田園染料植物巡禮，讓大家學習、認識可用來染色之植物，並因應時節進行簡單之農事操作或收割，再來將染料植物或食材進行調製、加工處理，並將染料植物入菜烹調，讓遊客自己體驗如何將染料植物入菜，烹調完成後便可自行享用自己烹調之菜色，用完餐後可至染工坊實際體驗天然植物染布過程，集學習、體驗、娛樂於一體。此外，在這裡也有許多精緻植物染精品可供挑選。",
          "City": "苗栗縣",
          "Town": "三義鄉",
          "Coordinate": "24.3914167,120.793373",
          "PicURL": "https://ezgo.coa.gov.tw/Uploads/opendata/TainmaMain01/APPLY_D/20151102094332.jpg"
        },
      ]
    }
  },
  methods: {
    changeMode(mode = '') {
      this.mode = mode;
    }
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