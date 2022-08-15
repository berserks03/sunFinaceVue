<template>
<div class="city container">
  <div class="city__background" :class="{'city__background--night' : !dayNight}" @click="dropdown = false"></div>

  <div class="city__inputContainer">
    <input
      type="text"
      class="city__input"
      autocomplete="off"
      placeholder="Type here city name"
      v-model="userInput"
      @focus="dropdown = true"
    >

    <Toggle
      enabled="C"
      disabled="F"
      :default="units"
      @set-val="setUnits"
    />
  </div>

  <Dropdown
    v-if="showDropdown"
    :cities="cities"
    @city-click=setInput
  />
  
  <Modal
    v-if="showModal"
    :city="city"
    :units="units"
    @close-modal="showModal=false"
  />

  <Toggle
      enabled="D"
      disabled="N"
      :default="units"
      @set-val="setDayNight"
      class="city__dayNight"
    />

</div>
</template>

<script lang="ts">
import Dropdown from '@/components/CitiesDropdown.vue'
import Modal from '@/components/CitiesModal.vue';
import Toggle from '@/components/Toggle.vue';
import { CitiesResponse, City } from "@/types/types";
import CitiesModel from '@/models/CitiesModel';
import Vue from 'vue';

export default Vue.extend({
  name: 'SearchComponent',
  components: {    
    Modal,
    Dropdown,
    Toggle,
  },
  data() {
    return {
      userInput: "" as string,
      dropdown: false as boolean,
      cities: [] as City[],
      city: {} as City,
      showModal: false as boolean,
      units: true as boolean,
      dayNight: true as boolean,
    }
  },
  methods: {
    fetchCities() {
      const urlbBeginig = "https://openweathermap.org/data/2.5/find?q=";
      const urlEnd = "&appid=439d4b804bc8187953eb36d2a8c26a02&units=" + this.whichUnits;
      const url = urlbBeginig+this.userInput+urlEnd;
      
      if (this.isEnoughLongInput) {
        fetch(url, {method: "GET", mode: 'cors'})
          .then(res => res.json())
          .then((data: CitiesResponse) => this.cities = CitiesModel.createFromCollection(data.list))
          .catch(err => console.log('Fetch Error :-S', err));
      }
    },
    setInput(city: City) {
      this.city = city;
      this.userInput = city.name;
      this.dropdown = false;
      this.showModal = true;
    },
    setUnits(val: boolean) {
      this.units = val;
    },
    setDayNight(val: boolean) {
      this.dayNight = val;
    },
  },
  computed: {
    showDropdown():boolean {
      return this.isCitiesNotEmpty && this.dropdown && this.isEnoughLongInput;
    },
    isCitiesNotEmpty(): boolean {
      return this.cities.length > 0;
    },
    isEnoughLongInput(): boolean {
      return this.userInput.length > 2;
    },
    whichUnits(): string {
      return this.units ? 'metric' : 'imperial';
    }
  },
  watch: {
    userInput() {
      this.fetchCities();
    },
  },
})
</script>

<style lang="scss" scoped>
.city {
  display: flex;
  flex-direction: column;
  align-items: center;

  &__background {
    position: absolute;
    top: 0px;
    right: 0px;
    bottom: 0px;
    left: 0px;
    z-index: 0;
    background-color: lightblue;

    &--night {
      background-color: black;
    }
  }

  &__inputContainer {
    z-index: 10;
    display: flex;
  }

  &__input {
    background-color: #d1d5db;
    padding: 0.5rem 1rem;
    border-radius: 16px;    
  }

  &__dayNight {
    position: absolute;
    right: 20%;
    top: 20%;
  } 
}
</style>
