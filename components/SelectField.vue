<template>
  <div class="select" :class="[selectWidth]">
    <div
      class="select__title"
      @click="areOptionsVisible = !areOptionsVisible"
    >
      {{ selected }}
    </div>
    <div class="select__options select-options" v-if="areOptionsVisible">
      <!-- <div
        class="select-options__item active"
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)"
      >
        {{ option.name }}
      </div> -->
      <div
        v-for="option in options"
        :key="option.value"
      >
        <template v-if="selectedConditions.find(item => item.value === option.value)">
          <div class="select-options__item">
            {{ option.name }}
          </div>
        </template>
        <template v-else>
          <div
            class="select-options__item active"
            @click="selectOption(option)"
          >
            {{ option.name }}
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      default () {
        return []
      }
    },
    selected: {
      type: String,
      default: ''
    },
    selectWidth: {
      type: String,
      default: ''
    },
    selectedConditions: Array
  },
  data () {
    return {
      areOptionsVisible: false
    }
  },
  methods: {
    selectOption (option) {
      this.$emit('select', option)
      this.areOptionsVisible = false
    },
    hideOptions () {
      this.areOptionsVisible = false
    }
  }
  // mounted () {
  //   document.addEventListener('click', this.hideOptions.bind(this), true)
  // },
  // beforeDestroy () {
  //   document.removeEventListener('click', this.hideOptions)
  // }
}
</script>

<style lang="scss" scoped>
.select {
  position: relative;
  height: 50px;
}

.select__title {
  display: flex;
  align-items: center;
  width: 100%;
  height: 100%;
  padding: 8px 16px;
  border-radius: $border-radius;
  border: solid 2px $border;
  font-size: 1.1rem;
  cursor: pointer;
  &::before,
  &::after {
    content: "";
    position: absolute;
    top: 50%;
    right: 16px;
    display: block;
    width: 10px;
    height: 2px;
    transition: all 0.3s ease-out;
    background-color: #333333;
    transform: translate(-3px, -50%) rotate(45deg);
  }
  &::after {
    transform: translate(3px, -50%) rotate(-45deg);
  }
  &:hover {
    border-color: $info;
    &::before,
    &::after {
      background-color: #333333;
    }
  }
}

.select__options {
  position: absolute;
  top: 55px;
  left: 0px;
  width: 100%;
  background-color: #ffffff;
  border: 2px solid $border;
  border-radius: 5px;
  transition: all 0.3s ease-out;
  z-index: 100;
}

.select-options__item {
  padding: .5rem 1rem;
  overflow: hidden;
}

.select-options__item.active:hover {
  background-color: #ada5a7;
  color: #fff;
  cursor: pointer;
}

.select-options__item:hover {
  cursor: no-drop;
}
</style>
