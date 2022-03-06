<template>
  <select class="BaseSelect" v-model="selectValue" @change="$emit('change', selectValue)">
    <option value="" disabled selected>{{ placeholder }}</option>
    <option v-for="option in options" :key="option.value" :value="option.value">
      {{ option.text }}
    </option>
  </select>
</template>

<script>
export default {
  props: {
    placeholder: {
      type: String,
      default: 'Choose'
    },
    options: {
      type: Array,
      /**
       * @param: [{value: string, text: string}]
       */
      default: () => ([]),
    }
  },
  data() {
    return {
      selectValue: ''
    }
  },
  watch: {
    options() {
      this.selectValue = ''
    }
  }
}
</script>
<style lang="scss" scoped>
.BaseSelect {
  border-width: 0;
  padding: .5rem;
  background-color: #d6d6d6;
}
</style>
