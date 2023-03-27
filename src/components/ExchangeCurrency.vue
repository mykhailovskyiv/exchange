<template>
 <div class="currency">
   <h4 class="title">Current exchange rate</h4>
   <div class="currency__container">
     <select class="currency__select" v-model="currencyValue" @change="changeCurrency">
       <option
         v-for="item in currency.slice(0,2)"
         :key="item.index"
         :value="item.code"
       >
         {{ item.code }}
       </option>
     </select>
     <div class="currency-exchange">
       <div class="currency-exchange__item" v-for="(value, name) in currentRate">
         <div>{{name}}</div>
         <div>{{value}}</div>
       </div>
     </div>
   </div>
 </div>
</template>

<script>
export default {
  name: "ExchangeCurrency",
  data() {
    return {
      currencyValue: "USD",
      currencyGet: [],
      currentRate: null,
    }
  },
  props: {
    currency: {
      type: Array,
      required: true
    }
  },
  methods: {
    changeCurrency() {
      this.currencyGet = []
      this.currency.forEach((item) => {
        this.currencyValue !== item.code ? this.currencyGet.push(item.code) : false
      })
      this.getCurrency()
    },
    getCurrency() {
      let currencyString = this.currencyGet.toString()
      fetch(`https://exchange-rates.abstractapi.com/v1/live/?api_key=a2528bb76fdf4236853bf722774e052c&base=${this.currencyValue}&target=${currencyString}`)
        .then(resp => resp.json())
        .then((resp) => {
          this.currentRate = resp.exchange_rates
        })

    }
  },
  mounted() {
    // this.changeCurrency()
  }
}
</script>

<style lang="scss">
 .currency {
   margin-top: 20px;
   &__container {
     background-color: rgb(255, 255, 255);
     border-radius: 10px;
     padding: 10px;
     margin-top: 10px;
   }
   &__select {
     padding: 5px 10px;
     border: none;
     border-radius: 10px;
     background-color: #000000;
     color: greenyellow;
   }
   &-exchange {
     display: flex;
     flex-direction: column;

     &__item {
       display: flex;
       justify-content: space-between;
       border-radius: 10px;
       background-color: #000000;
       margin-top: 10px;
       color: greenyellow;
       padding: 10px;
     }
   }
 }

</style>
