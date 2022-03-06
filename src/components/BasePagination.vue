<template>
  <div class="BasePagination" v-if="totalPageNumber > 0">
    <label class="BasePagination__label">{{`美食頁次 ${currentPage} / ${totalPageNumber}`}}</label>
    <div class="BasePagination__pages">
      <button
        class="BasePagination__button"
        :class="{'BasePagination__button--active': page === currentPage}"
        v-for="page in totalPageNumber"
        :key="page"
        @click="pageChangeHandler(page)"
      >
        {{ page }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    size: {
      type: Number,
      default: 10,
      validator (val) {
        return val > 0;
      }
    },
    total: {
      type: Number,
      default: 1
    },
    currentPage: {
      type: Number,
      default: 1
    }
  },
  computed: {
    totalPageNumber () {
      if (this.total <= 0) return 0; 
      return Math.ceil(this.total / this.size);
    }
  },
  methods: {
    pageChangeHandler (page = 1) {
      this.$emit('change-page', { page });
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/rwd.scss';
.BasePagination {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  &__label {
    @include mobile{
      display: none;
    }
  }
  &__pages {
    display: flex;
    flex-wrap: wrap;
  }
  &__button {
    margin-left: 1rem;
    outline: 0px;
    border-width: 0px;
    padding: .25rem .5rem;
    background-color: #dddddd;
    color: #adb3b3;
    cursor: pointer;
    &--active {
      background-color: #0ca2d4;
      color: white;
      cursor: not-allowed;
    }
  }
}
</style>