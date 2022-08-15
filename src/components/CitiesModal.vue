<template>
    <div class="city__modalContainer" @click="$emit('close-modal')">
      <div class="city__modal">
        <div class="city__name">
          {{city.dropdownText}} <img :src="city.flagText"/>
        </div>
        <div class="city__weatherIcon">
          <img :src="city.iconText">
        </div>
        <div class="city__day">
          {{new Date().toLocaleDateString("LV", {weekday: 'long'})}}
        </div>
        <div class="city__temp">
          <div v-if="units">
            {{city.tempC}}
          </div>
          <div v-else>
            {{city.tempF}}
          </div>
        </div>
        <div class="city__minMax">
          <div v-if="units">
            {{city.minMaxTextC}}
          </div>
          <div v-else>
            {{city.minMaxTextF}}
          </div>
        </div>
      </div>
    </div>
</template>

<script lang="ts">
import { City } from '@/types/types';
import Vue from 'vue';
import { PropType } from 'vue/types/v3-component-props';
export default Vue.extend({
  name: "ModalComponent",
  props: {
    city: {
      type: Object as PropType<City>,
      required: true,
      default: () => ({}),
    },
    units: {
      type: Boolean,
      required: true,
      default: true,
    }
  },
})
</script>

<style lang="scss" scoped>
.city {

  &__modalContainer {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 98;
    background-color: rgba(0, 0, 0, 0.3);
  }

  &__modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 99;    
    width: 100%;
    max-width: 400px;
    background-color: lightgray;
    border-radius: 16px;    
    padding: 25px;

    @media only screen and (max-width: 900px) {
      max-width: 60vw;
    }
  }
  
  &__name,
  &__temp {
    font-size: 26px;
  }

  &__day,
  &__temp,
  &__minMax {
    margin-top: 10px;
  }

  &__minMax {
    font-size: 14px;
    color: gray;
  }
}
</style>
