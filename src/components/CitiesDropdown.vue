<template>
  <div class="city__listContainer">
    <ul class="city__list">
      <li
        v-for="city in cities"
        :key=city.id
        class="city__listItem"
        @click="$emit('city-click', city)"
      >
        {{city.dropdownText}} <img :src="city.flagText"/>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { City } from '@/types/types'
import Vue from 'vue'
import { PropType } from 'vue/types/v3-component-props'
export default Vue.extend({
  name: 'DropdownComponent',
  props: {
    cities: {
      type: Array as PropType<City[]>,
      required: true,
      default: () => [],
    }
  },

})
</script>

<style lang="scss" scoped>
.city {

  &__listContainer {
    z-index: 10;    
    margin-left: -74px;
  }

  &__list {
    width: 12rem;
    background-color: #1f2937;
    color: white;
    list-style-type: none;
    margin: 0;
    padding: 0;
  }

  &__listItem {
    padding: 0 0.5rem;
    border-bottom-width: 1px;
    cursor: pointer;
  }
}
</style>
