<template>
  <div>
    <div class="container">
      <div class="breadcrumbs">
        <div class="breadcrumbs__item">
          <a href="#">
            <svg viewBox="0 0 30 30" preserveAspectRatio="xMidYMid meet" height="20">
              <path
                d="  M27,29H5V17H3.235c-1.138,0-1.669-1.419-0.812-2.168L14.131,3.745c1.048-0.993,2.689-0.993,3.737,0l11.707,11.087  C30.433,15.58,29.902,17,28.763,17H27V29z"
                fill="none"
                id="XMLID_1_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"/>
              <path
                d="  M20,29h-8v-6c0-2.209,1.791-4,4-4h0c2.209,0,4,1.791,4,4V29z"
                fill="none"
                id="XMLID_2_"
                stroke="#000000"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-miterlimit="10"
                stroke-width="2"/>
            </svg>
          </a>
        </div>
        <span class="breadcrumbs__divider"></span>
        <div class="breadcrumbs__item"><a href="#">Опросы</a></div>
        <span class="breadcrumbs__divider"></span>
        <div class="breadcrumbs__item">Добавить опрос</div>
      </div>
      <section>
        <ul class="tabs">
          <li v-on:click="activeTab=1" v-bind:class="[ activeTab == 1 ? 'is-active' : '' ]" class="tabs__item">Параметры</li>
          <li v-on:click="activeTab=2" v-bind:class="[ activeTab == 2 ? 'is-active' : '' ]" class="tabs__item">Вопросы</li>
          <li v-on:click="activeTab=3" v-bind:class="[ activeTab == 3 ? 'is-active' : '' ]" class="tabs__item">Логика</li>
          <li v-on:click="activeTab=4" v-bind:class="[ activeTab == 4 ? 'is-active' : '' ]" class="tabs__item">Условия</li>
          <li v-on:click="activeTab=5" v-bind:class="[ activeTab == 5 ? 'is-active' : '' ]" class="tabs__item">Респонденты</li>
        </ul>
        <div class="tabs-content">
          <div v-if="activeTab == 1"  class="tabs-content__item"><h3 class="tabs-content__title mt-0">Параметры</h3></div>
          <div v-if="activeTab == 2"  class="tabs-content__item"><h3 class="tabs-content__title mt-0">Вопросы</h3></div>
          <div v-if="activeTab == 3"  class="tabs-content__item"><h3 class="tabs-content__title mt-0">Логика</h3></div>
          <div v-if="activeTab == 4"  class="tabs-content__item"><h3 class="tabs-content__title mt-0">Условия</h3></div>
          <div v-if="activeTab == 5"  class="tabs-content__item tabs-content-item">
            <form @submit.prevent="postData" method="post">
              <h3 class="tabs-content__title mt-0">Добавить опрос</h3>
              <Condition
                v-for="(conditionQuantity, i) in conditionsQuantity"
                :conditionQuantity="conditionQuantity"
                :index="i"
                :conditions="conditions"
                :key="conditionQuantity.id"
                :selectedConditions="selectedConditions"
                @remove-condition="removeCondition"
                @respondent="addRespondent"
                @selectedCondition="selectedCondition"
              />
              <div @click="addCondition" class="tabs-content-item__section tabs-content-item__button">
                <div class="poll-adding-button">
                  <svg class="poll-adding-button__icon" viewBox="0 0 30 30" preserveAspectRatio="xMidYMid meet" height="40">
                    <defs>
                      <style>.cls-1{fill:none;stroke:#000;stroke-linecap:round;stroke-linejoin:round;stroke-width:2px;}</style>
                    </defs>
                    <title/>
                    <g id="plus">
                      <line class="cls-1" x1="16" x2="16" y1="7" y2="25"/>
                      <line class="cls-1" x1="7" x2="25" y1="16" y2="16"/>
                    </g>
                  </svg>
                  <p class="poll-adding-button__text mt-0">Нажмите, чтобы добавить новое условие выборки.<br/>Все условия связываются между собой логическим "И"</p>
                </div>
              </div>
              <div class="tabs-content-item__section">
                <div class="row is-space-between">
                  <div class="form__button form__button--white">Протестировать опрос</div>
                  <button
                    v-if="Object.keys(respondents).find(key => respondents[key].length > 0)"
                    class="form__button form__submit"
                    type="submit"
                  >
                    <span>Далее</span>
                    <svg class="form-button__icon ml-1" viewBox="0 0 30 30" preserveAspectRatio="xMidYMid meet" height="20">
                      <defs>
                        <style>.cls-1{fill:none;}</style>
                      </defs>
                      <title/>
                      <g data-name="Layer 2" id="Layer_2">
                        <path d="M19,26a1,1,0,0,1-.71-.29,1,1,0,0,1,0-1.42L26.59,16l-8.3-8.29a1,1,0,0,1,1.42-1.42l9,9a1,1,0,0,1,0,1.42l-9,9A1,1,0,0,1,19,26Z"/>
                        <path d="M28,17H4a1,1,0,0,1,0-2H28a1,1,0,0,1,0,2Z"/>
                      </g>
                    </svg>
                  </button>
                  <button
                    v-else
                    class="form__button form__submit form__submit--disabled"
                    type="button"
                    disabled
                  >
                    <span>Далее</span>
                    <svg class="form-button__icon ml-1" viewBox="0 0 30 30" preserveAspectRatio="xMidYMid meet" height="20">
                      <defs>
                        <style>.cls-1{fill:none;}</style>
                      </defs>
                      <title/>
                      <g data-name="Layer 2" id="Layer_2">
                        <path d="M19,26a1,1,0,0,1-.71-.29,1,1,0,0,1,0-1.42L26.59,16l-8.3-8.29a1,1,0,0,1,1.42-1.42l9,9a1,1,0,0,1,0,1.42l-9,9A1,1,0,0,1,19,26Z"/>
                        <path d="M28,17H4a1,1,0,0,1,0-2H28a1,1,0,0,1,0,2Z"/>
                      </g>
                    </svg>
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      activeTab: 5,
      conditions: [
        { id: 1, name: 'Возраст респондента', value: 'ConditionRange', text: 'диапазон', color: '#A37200' },
        { id: 2, name: 'Тип карты лояльности', value: 'ConditionType', text: 'тип', color: '#2248A6' },
        { id: 3, name: 'Статус карты лояльности', value: 'ConditionStatus', text: 'статус', color: '#6DA622' }
      ],
      conditionsQuantity: [
        { id: 1 }
      ],
      selectedConditions: []
    }
  },
  computed: {
    respondents () {
      const respondents = {}
      for (let i = 0; i < this.conditions.length; i++) {
        const condition = this.conditions[i]
        respondents[condition.value] = []
      }
      return respondents
    }
  },
  methods: {
    selectedCondition ({ id, value }) {
      if (!this.selectedConditions.find(item => item.id === id)) {
        const temp = {
          id,
          value
        }
        this.selectedConditions.push(temp)
      } else {
        const current = this.selectedConditions.find(item => item.id === id)
        current.value = value
      }
    },
    addCondition () {
      this.conditionsQuantity.push({ id: Math.floor(Math.random() * (Math.floor(1000 - Math.ceil(2) + 1))) + Math.ceil(2) })
    },
    removeCondition ({ id, value }) {
      this.conditionsQuantity = this.conditionsQuantity.filter(c => c.id !== id)
      this.respondents[value] = []
      this.selectedConditions = this.selectedConditions.filter(c => c.value !== value)
    },
    addRespondent ({ currentCondition, value }) {
      if (this.respondents[currentCondition].find(item => item.id === value.id)) {
        const foundIndex = this.respondents[currentCondition].findIndex(x => x.id === value.id)
        this.respondents[currentCondition][foundIndex] = value
        this.$nextTick(function () {
          this.$forceUpdate()
        })
      } else {
        this.respondents[currentCondition].push(value)
        this.respondents[currentCondition] = [...new Set(this.respondents[currentCondition])]
        this.$nextTick(function () {
          this.$forceUpdate()
        })
      }
    },
    postData () {
      this.$axios.$post('/polls', this.respondents).then((res) => {
        // Perform Success Action
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.breadcrumbs {
  font-size: 14px;
  color: #afafaf;
}

.breadcrumbs__item {
  display: inline-block;
  vertical-align: middle;
}

.breadcrumbs__divider {
  display: inline-block;
  position: relative;
  width: 1rem;
  height: 1rem;
  vertical-align: middle;
}

.breadcrumbs__divider::before {
  content: '';
  position: absolute;
  display: block;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: url('/breadcrumbs-divider.svg') center no-repeat;
  background-size: contain;
  width: 14px;
  height: 14px;
}

.tabs {
  display: flex;
  justify-content: flex-start;
  flex-wrap: nowrap;
  margin-bottom: 0;
  border-bottom: 1px solid #C1E837;
  color: $success;
}

.tabs__item {
  position: relative;
  cursor: pointer;
  transition: all .1s;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  padding: 1rem 3rem;
}

.tabs__item.is-active {
  color: $primary;
  font-weight: 700;
}

.tabs__item:hover::after,
.tabs__item.is-active::after {
  content: '';
  display: block;
  position: absolute;
  left: 0;
  bottom: 0px;
  width: 100%;
  height: 3px;
  background: #C1E837;
  transition: all .1s;
}

.tabs-content {
  border-radius: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
  box-shadow: 0 10px 15px rgb(0 0 0 / 10%);
  background-color: #fafafa;
}

.tabs-content__title {
  font-size: 1.2rem;
  font-weight: 700;
  color: $secondary;
  padding: 2.5rem;
  padding-bottom: 1rem;
  margin-bottom: 0;
}

.tabs-content-item__section {
  padding: 2.5rem;
}

.tabs-content-item__button {
  background-color: #fff;
}

.poll-adding-button {
  padding: 1rem;
  text-align: center;
  border: 2px solid $border;
  border-radius: 5px;
  color: $info-darkest;
  font-size: 1.1rem;
  line-height: 1.5rem;
  cursor: pointer;
  transition: all .1s;
}

.poll-adding-button__icon line {
  stroke: $info-darkest;
}

.poll-adding-button:hover {
  border: 2px solid $info-darkest;
}

.form__button {
  display: flex;
  padding: .8rem 1rem;
  color: $primary;
  font-size: 1.1rem;
  border-radius: $border-radius;
  justify-content: center;
  align-items: center;
  height: 3.2rem;
  line-height: 3.2rem;
  cursor: pointer;
  transition: all .1s;
}

.form__button--white {
  background-color: #fff;
  color: $info-darkest;
  box-shadow: 0 3px 3px rgb(0 0 0 / 20%);
}

.form__submit {
  background-color: #06A326;
  color: #fff;
  font-size: 1.2rem;
  border: 0;
}

.form__submit:hover {
  background-color: $info-darkest;
}

.form__submit--disabled {
  background-color: $secondary;
  cursor: no-drop;
}

.form__submit--disabled:hover {
  background-color: $secondary;
}

.form-button__icon path {
  stroke: #fff;
  fill: #fff;
}

.form__button--green path,
.form__button--green line {
  stroke: $info-dark;
}

.form__button.form__button--white:hover {
  box-shadow: 0 2px 2px rgb(0 0 0 / 20%);
}

.form__button--green:hover {
  border-color: $info-dark;
}

.tabs-content-item__section-divider {
  border-top: 1px solid $border;
  position: relative;
}

.tabs-content-item__section-divider::before {
  position: absolute;
  content: 'и';
  display: block;
  top: 0;
  left: 40px;
  transform: translate(0, -50%);
  border-radius: 8px;
  margin-right: 1rem;
  height: 50px;
  line-height: 50px;
  width: 60px;
  text-align: center;
  font-size: 1.1rem;
  background-color: #E5F0FA;
  text-transform: uppercase;
}
</style>
