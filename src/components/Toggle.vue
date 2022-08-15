<template>
  <label class="switch">
    <input type="checkbox" @click="toggleCheckbox" class="switch__input">
    <div class="switch__slider switch__slider--round">
    <transition name="fade">
      <span class="switch__active" v-if="checkbox">{{enabled}}</span>
    </transition>
    <transition name="fade">
      <span class="switch__inactive" v-if="!checkbox">{{disabled}}</span>
    </transition>
    </div>
  </label>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'ToggleComponent',
  props: {
    default: {
      type: Boolean,
      default: false,
    },
    enabled: {
      type: String,
      default: 'On',
    },
    disabled: {
      type: String,
      default: 'Off',
    }
  },
  data() {
    return {
      checkbox: this.default,
    }
  },
  methods: {
    toggleCheckbox() {
      this.checkbox = !this.checkbox
      this.$emit('set-val', this.checkbox)
    },
  },
})
</script>

<style lang="scss" scoped>
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  margin-left: 15px;

  &__input {
    display: none;

    &:checked + .switch__slider {
      background-color: #101010;
    }

    &:focus + .switch__slider {
      box-shadow: 0 0 1px #101010;
    }

    &:checked + .switch__slider:before {
      content: "";
      -webkit-transform: translateX(26px);
      -ms-transform: translateX(26px);
      transform: translateX(26px);
    }
  }

  &__slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    -webkit-transition: 0.4s;
    transition: 0.4s;

    &--round {
      border-radius: 34px;
    }

    &--round:before {
      border-radius: 50%;
    }

    &:before {
      line-height: 26px;
      position: absolute;
      content: "";
      height: 26px;
      width: 26px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      -webkit-transition: 0.4s;
      transition: 0.4s;
    }
  }

  &__active {
    position: absolute;
    top: 9px;
    left: 11px;
  }

  &__inactive {
    position: absolute;
    top: 9px;
    right: 11px;
  }
}

.fade-enter-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
