<template>
  <div class="modal">
    <div class="modal-content">
      <span class="close" @click="closeModal">&times;</span>
      <div class="modal-wrapper">
        <select v-model="currency" class="modal-wrapper__select">
          <option v-for="item in filteredCurrency" :value="item">{{ item.name }}</option>
        </select>
        <button @click="addNewCurrency" class="modal-wrapper__button">Add to table</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      currency: {}
    }
  },
  props: {
    filteredCurrency: {
      type: Array,
      required: true
    }
  },
  methods: {
    addNewCurrency() {
      this.$emit('addNewCurrency', this.currency)
    },
    closeModal() {
      this.$emit('closeModal', false)
    }
  }
}
</script>

<style lang="scss">

.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  position: relative;
  background-color: #fefefe;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0,0,0,0.3);
  width: 80%;
}

.close {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 24px;
  cursor: pointer;
  color: black;
}
.modal-wrapper {
  width: 90%;
  display: flex;
  flex-direction: column;
  align-items: center;
  &__select {
    width: 80%;
    border: none;
    text-align: center;
    background: black;
    color: greenyellow;
    border-radius: 10px;
    padding: 5px;
  }
  &__button {
    padding: 5px 10px;
    border: none;
    border-radius: 10px;
    background-color: #000000;
    color: greenyellow;
    margin-top: 10px;
    width: 40%;
  }
}
@media(min-width: 1100px) {
  .modal-content {
    width: 1000px;
  }
  .modal-wrapper {
    padding: 20px;
    &__select, &__button {
      padding: 10px;
      font-size: 15px;
    }

  }
}

</style>
