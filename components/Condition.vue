<template>
  <div class="tabs-content-item__section" :class="[index > 0 ? 'tabs-content-item__section-divider' : '']">
    <div class="row is-align-centered mb-5">
      <div class="polls-form__label col-4" :style="{color: selectedColor}">Условие {{ index + 1 }}</div>
      <SelectField
        :options="conditions"
        @select="optionSelect"
        :selected="selected"
        :selectWidth="selectWidth"
        :selectedConditions="selectedConditions"
      />
    </div>
    <component
      :is="currentCondition"
      v-for="(select, i) in currentConditionSelects"
      :key="select.id"
      :select="select"
      :index="i"
      @condition="addCondition"
      :selectedConditionTypes="selectedConditionTypes"
      @selectedConditionType="selectedConditionType"
    ></component>
    <div class="row is-right">
      <div class="col-8">
        <div class="row is-space-between">
          <div v-if="currentCondition" @click="addSelects" class="form__button form__button--green form-button">
            <svg class="form-button__icon mr-1" viewBox="0 0 30 30" preserveAspectRatio="xMidYMid meet" height="25">
              <defs>
                <style>.cls-1{fill:none;stroke:#000;stroke-linecap:round;stroke-linejoin:round;stroke-width:2px;}</style>
              </defs>
              <title/>
              <g id="plus">
                <line class="cls-1" x1="16" x2="16" y1="7" y2="25"/>
                <line class="cls-1" x1="7" x2="25" y1="16" y2="16"/>
              </g>
            </svg>
            <span class="form-button__text">Добавить {{ conditionText }}</span>
          </div>
          <div @click="$emit('remove-condition', {id: conditionQuantity.id, value: currentCondition})" class="form__button form__button--red form__button--rigth form-button">
            <svg viewBox="0 0 30 30" preserveAspectRatio="xMidYMid meet" height="23" class="form-button__icon mr-1">
              <path
                d="  M25,10H7v17c0,1.105,0.895,2,2,2h14c1.105,0,2-0.895,2-2V10z"
                fill="none"
                id="XMLID_129_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"/>
              <path
                d="  M20,7h-8V5c0-1.105,0.895-2,2-2h4c1.105,0,2,0.895,2,2V7z"
                fill="none"
                id="XMLID_145_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"/>
              <path
                d="  M28,10H4V8c0-0.552,0.448-1,1-1h22c0.552,0,1,0.448,1,1V10z"
                fill="none"
                id="XMLID_146_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"/>
              <line
                fill="none"
                id="XMLID_148_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"
                x1="16"
                x2="16"
                y1="15"
                y2="24"/>
              <line
                fill="none"
                id="XMLID_147_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"
                x1="12"
                x2="12"
                y1="15"
                y2="24"/>
              <line
                fill="none"
                id="XMLID_149_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"
                x1="20"
                x2="20"
                y1="15"
                y2="24"/>
            </svg>
            <span class="form-button__text">Удалить условие</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    conditionQuantity: Object,
    index: Number,
    conditions: Array,
    selectedConditions: Array
  },
  data () {
    return {
      selected: 'Выберите условие',
      selectedColor: '',
      currentConditionSelects: [
        { id: 1 }
      ],
      currentCondition: '',
      conditionText: '',
      selectWidth: 'col-8',
      selectedConditionTypes: []
    }
  },
  methods: {
    selectedConditionType ({ id, value }) {
      if (!this.selectedConditionTypes.find(item => item.id === id)) {
        const temp = {
          id,
          value
        }
        this.selectedConditionTypes.push(temp)
      } else {
        const current = this.selectedConditionTypes.find(item => item.id === id)
        current.value = value
      }
    },
    optionSelect (option) {
      this.selected = option.name
      this.selectedColor = option.color
      this.currentCondition = option.value
      this.$emit('selectedCondition', { id: this.index + 1, value: option.value })
      this.conditionText = option.text
      this.currentConditionSelects = [
        { id: 1 }
      ]
    },
    addSelects () {
      this.currentConditionSelects.push({ id: Math.floor(Math.random() * (Math.floor(1000 - Math.ceil(2) + 1))) + Math.ceil(2) })
    },
    addCondition (value) {
      this.$emit('respondent', { currentCondition: this.currentCondition, value })
    }
  }
}
</script>

<style lang="scss" scoped>
.polls-form__label {
  font-size: 1.2rem;
  font-weight: 700;
  color: #000;
}

.polls-form__input {
  border: 2px solid $border;
  color: #afafaf;
  border-radius: $border-radius;
  outline: none;
  padding: 0 1rem;
  height: 3.2rem;
  line-height: 3.2rem;
  width: 110px;
}

.polls-form__span {
  font-size: 1.1rem;
}

.form__button {
  display: flex;
  padding: .8rem 1rem;
  color: $primary;
  font-size: 1.1rem;
  border: 2px solid #ccc;
  border-radius: $border-radius;
  justify-content: center;
  align-items: center;
  height: 3.2rem;
  line-height: 3.2rem;
  cursor: pointer;
  transition: all .1s;
}

.form__button--rigth {
  margin-left: auto;
}

.form__button--red {
  border-color: $danger;
  color: $danger-dark;
}

.form__button--green {
  border-color: $info;
  color: $info-dark;
}

.form-button__icon path,
.form-button__icon line {
  stroke: $danger-dark;
}

.form__button--green path,
.form__button--green line {
  stroke: $info-dark;
}

.form__button:hover {
  border-color: $danger-dark;
}

.form__button--green:hover {
  border-color: $info-dark;
}
</style>
