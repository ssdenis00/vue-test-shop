<template>
  <header class="header">
    <Menu />
    <Search v-on:getInputValue="getInputValue" />
  </header>
</template>

<script>
import Menu from "../Menu/Menu.vue";
import Search from "../Search/Search.vue";

export default {
  name: "Header",
  components: {
    Menu,
    Search,
  },
  methods: {
    getInputValue(res) {
      this.$emit("getInputValue", res);
    },
  },
};
</script>

<style src="./Header.css"></style>
