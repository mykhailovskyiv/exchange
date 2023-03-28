<template>
  <div class="exchange">
    <div class="exchange__container">
      <input
        v-model="inputOne"
        @input="getFirstCurrency"
        type="number"
        class="exchange__input"
      >
      <select class="exchange__select" v-model="currentOne" @change="handleSelectChange">
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
        v-model="inputTwo"
        @input="getSecondCurrency"
        type="number"
        class="exchange__input"
      >
      <select class="exchange__select" v-model="currentTwo" @change="handleSelectChange">
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
import { debounce } from 'lodash';

export default {
  name: "ExchangeSelect",
  data() {
    return {
      inputOne: 1,
      inputTwo: null,
      currentOne: "USD",
      currentTwo: "EUR",
      prevOne: "USD",
      prevTwo: "EUR"
    }
  },
  props: {
    currency: {
      type: Array,
      required: true
    }
  },
  mounted() {
    fetch(`https://exchange-rates.abstractapi.com/v1/convert?api_key=a2528bb76fdf4236853bf722774e052c&base=${this.currentOne}&target=${this.currentTwo}&&base_amount=${this.inputOne}`)
      .then(resp => resp.json())
      .then((resp) => {
        this.inputTwo = resp.converted_amount
      })
  },
  methods: {
    handleSelectChange: function () {
      if (this.currentOne === this.currentTwo) {
        this.currentTwo = this.prevOne;
        this.currentOne = this.prevTwo;
      } else if (this.currentOne === this.prevTwo && this.currentTwo === this.prevOne) {
        this.currentOne = this.prevTwo;
        this.currentTwo = this.prevOne;
      }
      this.prevOne = this.currentOne;
      this.prevTwo = this.currentTwo;
      this.inputOne = 1
      this.getFirstCurrency()
    },
    getFirstCurrency: debounce(function () {
        fetch(`https://exchange-rates.abstractapi.com/v1/convert?api_key=a2528bb76fdf4236853bf722774e052c&base=${this.currentOne}&target=${this.currentTwo}&&base_amount=${this.inputOne}`)
        .then(resp => resp.json())
        .then((resp) => {
          this.inputTwo = resp.converted_amount
        })}, 1000),

    getSecondCurrency: debounce(function () {
        fetch(`https://exchange-rates.abstractapi.com/v1/convert?api_key=a2528bb76fdf4236853bf722774e052c&base=${this.currentTwo}&target=${this.currentOne}&&base_amount=${this.inputTwo}`)
        .then(resp => resp.json())
        .then((resp) => {
          this.inputOne = resp.converted_amount
        })}, 1000)
  },
  watch: {
    inputOne(val) {
     this.inputOne = val >= 10000 ? 10000 : val
     this.inputOne = !val ? 1 : val
    },
    inputTwo(val) {
      this.inputTwo = val >= 10000 ? 10000 : val
      this.inputTwo = !val ? 1 : val
    },
  }
}
</script>

<style lang="scss">
.exchange {
  margin: 0 auto;
  margin-top: 20px;
  padding: 10px;
  border-radius: 10px;
  background-color: white;
  &__container {
    margin-top: 10px;
    border: 1px solid;
    border-radius: 10px;
    padding: 10px 5px;
    display: flex;
    justify-content: space-between;
    background-color: black;
  }
  &__input {
    border: none;
    width: 70%;
    padding-left: 10px;
    background: black;
    color: greenyellow;
    outline: none;

  }
  &__select {
    border: none;
    width: 30%;
    text-align: center;
    background: black;
    color: greenyellow;
  }

}
@media(min-width: 426px) {
  .exchange {
    display: flex;
    justify-content: space-between;
    &__container {
      width: 47%;
    }
  }
}

</style>
