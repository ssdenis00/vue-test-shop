<template>
  <ul class="card-list">
    <Card
      v-for="product of products"
      :key="product.id"
      v-bind:product="product"
      v-bind:selectedProducts="selectedProducts"
      v-bind:loader="loader"
      @selectProduct="selectProduct"
      @openModal="openModal"
      @getDataForModal="getDataForModal"
    />
  </ul>
</template>

<script>
import Card from "../Card/Card.vue";

export default {
  name: "CardList",
  props: ["products", "selectedProducts", "loader"],
  components: {
    Card,
  },
  methods: {
    selectProduct(res) {
      this.$emit("selectProduct", res);
    },
    openModal() {
      this.$emit("openModal", true);
    },

    getDataForModal(data) {
      this.$emit("getDataForModal", data);
    },
  },
};
</script>

<style src="./CardList.css"></style>
