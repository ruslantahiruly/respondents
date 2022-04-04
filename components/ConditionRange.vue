<template>
  <div class="row is-align-centered mb-5">
    <div class="polls-form__label-select col-4">
      <span v-if="index > 0" class="polls-form__logic polls-form__logic--or">или</span>
      <span>Диапазон {{ index + 1 }}</span>
    </div>
    <div>
      <span class="polls-form__span mr-1">от</span>
      <input type="number" class="polls-form__input mr-2" v-model="conditionRange.from" min="0">
      <span class="polls-form__span mr-1">до</span>
      <input type="number" class="polls-form__input mr-2" v-model="conditionRange.to" :min="conditionRange.from" @input="setRange()">
    </div>
  </div>
</template>

<script>
export default {
  props: {
    select: Object,
    index: Number
  },
  data () {
    return {
      conditionRange: {
        id: this.index + 1,
        from: null,
        to: null
      }
    }
  },
  methods: {
    setRange () {
      this.$emit('condition', this.conditionRange)
    }
  }
}
</script>

<style lang="scss" scoped>
.polls-form__label-select {
  font-size: 1.1rem;
  color: #000;
}

.polls-form__span {
  font-size: 1.1rem;
}

.polls-form__input {
  border: 2px solid $border;
  color: #000;
  border-radius: $border-radius;
  outline: none;
  padding: 0 1rem;
  height: 3.2rem;
  line-height: 3.2rem;
  width: 110px;
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
