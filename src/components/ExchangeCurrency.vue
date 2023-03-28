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
     <button @click="showModal = !showModal" class="currency__button">Add new currency</button>
   </div>
   <Modal
     v-if="showModal"
     :filteredCurrency="filteredCurrency"
     @addNewCurrency="addNewCurrency"
     @closeModal="closeModal"
   >
   </Modal>
 </div>
</template>

<script>
import Modal from "./Modal";
export default {
  name: "ExchangeCurrency",
  data() {
    return {
      currencyValue: "USD",
      defaultCurrency: [
        {
          code: "USD",
          name: "American Dollar",
        },
        {
          code: "EUR",
          name: "Euro",
        },
        {
          code: "ETH",
          name: "Ethereum",
        },
        {
          code: "BCH",
          name: "Bitcoin Cash",
        },
      ],
      currencyGet: [],
      currentRate: null,
      showModal: false
    }
  },
  props: {
    currency: {
      type: Array,
      required: true
    }
  },
  components: {
    Modal
  },
  created() {
    const itemsInLocalStorage = localStorage.getItem("items");
    if (itemsInLocalStorage) {
      this.defaultCurrency = JSON.parse(itemsInLocalStorage);
    }
    this.changeCurrency()
  },
  methods: {
    changeCurrency() {
      this.currencyGet = []
      this.defaultCurrency.forEach((item) => {
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

    },
    addNewCurrency(item) {
      this.defaultCurrency.push(item)
      this.showModal = false
      localStorage.setItem("items", JSON.stringify(this.defaultCurrency));
      this.changeCurrency()
    },
    closeModal(close) {
      this.showModal = close
    }
  },
  computed: {
    filteredCurrency() {
      return this.currency.filter((item) => {
        return !this.defaultCurrency.find((i) => i.code === item.code);
      });
    },
  },
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
   &__button {
     padding: 5px 10px;
     border: none;
     border-radius: 10px;
     background-color: #000000;
     color: greenyellow;
     margin-top: 10px;
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
 @media(min-width: 1100px) {
   .currency {
     &__select, &__button {
       padding: 7px 15px;
       font-size: 15px;
     }

   }
 }

</style>
