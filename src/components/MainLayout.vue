<template>
 <div class="container">
   <h2>Currency Exchange</h2>
   <div class="currency">
     <div class="currency__container">
       <input
         v-model="currencyValue"
         type="number"
         class="currency__input"
       >
       <select>
         <option
           v-for="item in currency"
           :key="item.index"
           :value="item.name"
           class="currency__select"
         >
           {{ item.code }}
         </option>
       </select>
     </div>
     <div class="currency__container">
       <input
         v-model="currencyValue"
         type="number"
         class="currency__input"
       >
       <select>
         <option
           v-for="item in currency"
           :key="item.index"
           :value="item.name"
           class="currency__select"
         >
           {{ item.code }}
         </option>
       </select>
     </div>
   </div>
 </div>
</template>

<script>
import currency from '../assets/currency.json'
export default {
  name: "MainLayout",
  data() {
    return {
      currency: currency,
      currencyValue: 100
    }
  }
}
</script>

<style scoped>

</style>
