<template>
  <div class="row is-align-centered mb-5">
    <div class="polls-form__label col-4">
      <span v-if="index > 0" class="polls-form__logic polls-form__logic--or">или</span>
      <span>Тип {{ index + 1 }}</span>
    </div>
    <SelectField
      :options="conditionTypes"
      @select="optionSelect"
      :selected="selected"
      :selectWidth="selectWidth"
      :selectedConditions="selectedConditionTypes"
    />
  </div>
</template>

<script>
export default {
  props: {
    select: {
      type: Object,
      required: true
    },
    index: Number,
    selectedConditionTypes: Array
  },
  data () {
    return {
      selected: 'Выберите тип',
      conditionTypes: [
        { name: 'Classic', value: 'classic' },
        { name: 'Gold', value: 'gold' },
        { name: 'Platinum', value: 'platinum' }
      ],
      areTypeVisible: false,
      selectWidth: 'col-7',
      conditionType: {
        id: this.index + 1,
        value: ''
      }
    }
  },
  // computed: {
  //   selected () {
  //     return this.conditionTypes[0]
  //   }
  // },
  methods: {
    optionSelect (option) {
      this.selected = option.name
      this.conditionType.value = option.value
      this.$emit('condition', this.conditionType)
      this.$emit('selectedConditionType', { id: this.index + 1, value: option.value })
    },
    selectType (option) {
      this.$emit('select', option)
      this.areOptionsVisible = false
    },
    hideTypes () {
      this.areOptionsVisible = false
    }
  },
  mounted () {
    document.addEventListener('click', this.hideTypes.bind(this), true)
  },
  beforeDestroy () {
    document.removeEventListener('click', this.hideTypes)
  }
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
}

.select-options__item {
  padding: .5rem 1rem;
  overflow: hidden;
}

.select-options__item:hover {
  background-color: #ada5a7;
  color: #fff;
  cursor: pointer;
}

.polls-form__logic {
  display: inline-block;
  border-radius: 8px;
  margin-right: 1rem;
  height: 50px;
  line-height: 50px;
  width: 60px;
  text-align: center;
  font-size: 1.1rem;
}

.polls-form__logic--or {
  background-color: #F7F1E3;
}

.polls-form__logic--and {
  background-color: #E5F0FA;
}
</style>
