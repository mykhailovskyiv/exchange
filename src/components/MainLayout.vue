<template>
 <div class="container">
   <img src="dollar.svg" alt="icon" width="35px">
   <h2 class="title">Currency Exchange</h2>
   <exchange-select :currency="currency"></exchange-select>
   <exchange-currency :currency="currency"></exchange-currency>
 </div>
</template>

<script>
import currency from '../assets/currency_codes.json'
import ExchangeSelect from "./ExchangeSelect";
import ExchangeCurrency from "./ExchangeCurrency";
export default {
  name: "MainLayout",
  components: {ExchangeCurrency, ExchangeSelect},
  data() {
    return {
      currency: currency,
    }
  },
  comments: {
    ExchangeSelect
  }
}
</script>

<style lang="scss">
  .container {
    margin: 0 auto;
    margin-top: 20px;
    width: 90%;
    .title {
      color: #ffffff;
    }
  }
  @media(min-width: 1100px) {
    .container {
      width: 1000px;
    }
  }

</style>
