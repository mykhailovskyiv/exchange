<template>
 <div class="currency">
   <div>
     <h4>Current exchange rate</h4>
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


 </div>
</template>

<script>
export default {
  name: "ExchangeCurrency",
  props: {
    data() {
      return {

      }
    },
    currency: {
      type: Array,
      required: true
    }
  },
}
</script>

<style scoped>

</style>
