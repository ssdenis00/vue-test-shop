<template>
  <main class="main">
    <h1 class="main__title">Картины эпохи Возрождения</h1>
    <section class="section">
      <CardList
        v-bind:products="products"
        @selectProduct="selectProduct"
        v-bind:selectedProducts="selectedProducts"
        v-bind:loader="loader"
        @openModal="openModal"
        @getDataForModal="getDataForModal"
      />
    </section>
  </main>
</template>

<script>
import CardList from "../CardList/CardList.vue";

export default {
  name: "Main",
  props: ["products", "selectedProducts", "loader"],
  components: {
    CardList,
  },
  methods: {
    selectProduct(res) {
      this.$emit("selectProduct", res);
    },
    openModal(data) {
      this.$emit("openModal", true);
    },

    getDataForModal(data) {
      this.$emit("getDataForModal", data);
    },
  },
};
</script>

<style src="./Main.css"></style>
