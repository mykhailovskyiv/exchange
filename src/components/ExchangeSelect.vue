<template>
  <div class="exchange">
    <div class="exchange__container">
      <input
        v-model="currencyValue"
        type="number"
        class="exchange__input"
      >
      <select class="exchange__select" v-model="currencyOne">
        <option
          v-for="item in currency"
          :key="item.index"
          :value="item.code"
        >
          {{ item.code }}
        </option>
      </select>
    </div>
    <div class="exchange__container">
      <input
        type="number"
        class="exchange__input"
      >
      <select class="exchange__select" v-model="currencyTwo">
        <option
          v-for="item in currency"
          :key="item.index"
          :value="item.code"
        >
          {{ item.code }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>

export default {
  name: "ExchangeSelect",
  data() {
    return {
      currencyValue: 100,
      currencyOne: "USD",
      currencyTwo: "EUR"
    }
  },
  props: {
    currency: {
      type: Array,
      required: true
    }
  },
  watch: {
    currencyValue(val) {
     this.currencyValue = val >= 10000 ? 10000 : val
    }
  }
}
</script>

<style lang="scss">
.exchange {
  margin: 0 auto;
  margin-top: 20px;
  &__container {
    margin-top: 10px;
    border: 1px solid;
    border-radius: 10px;
    padding: 10px 5px;
    display: flex;
    justify-content: space-between;
    background-color: white;
  }
  &__input {
    border: none;
    width: 70%;
    padding-left: 10px;

  }
  &__select {
    border: none;
    width: 30%;
    text-align: center;
  }

}

</style>
