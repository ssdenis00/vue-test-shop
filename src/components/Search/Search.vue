<template>
  <form @submit.prevent="getInputValue" action="/" class="form">
    <input
      type="text"
      class="form__input"
      placeholder="Поиск по названию картины"
      v-model="inputResult"
      @keyup="getInputValue"
    />
    <button type="submit" class="form__btn button">Найти</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      inputResult: "",
    };
  },
  methods: {
    getInputValue() {
      this.$emit("getInputValue", this.inputResult);
    },
  },
};
</script>

<style src="./Search.css"></style>
