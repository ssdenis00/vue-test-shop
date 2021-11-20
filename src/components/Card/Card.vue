<template>
  <li
    class="card-list__item"
    v-bind:class="{ 'card-list__item_disabled': !product.available }"
  >
    <img
      :src="product.images[0]"
      :alt="'постер ' + product.title"
      class="card-list__img"
      v-bind:class="{ 'card-list__img_disabled': !product.available }"
      @click="openModal"
    />
    <h2
      @click="openModal"
      class="card-list__title"
      v-bind:class="{ 'card-list__title_disabled': !product.available }"
    >
      {{ product.title }}
    </h2>
    <div class="card-list__price">
      <div class="card-list__cost-block">
        <p class="card-list__cost card-list__cost_type_sale">
          {{ product.available ? product.lastCost : "" }}
        </p>
        <p class="card-list__cost">
          {{ product.available ? product.cost : "Продана на аукционе" }}
        </p>
      </div>
      <button
        @click="selectProduct"
        type="button"
        class="card-list__btn button"
        v-bind:class="{
          'card-list__btn_type_selected': isSelected,
          'card-list__btn_hidden': !product.available,
        }"
      >
        {{
          (!isSelected && !loader) || (!isSelected && loader)
            ? "Купить"
            : loader && lastSelected
            ? "Ждем..."
            : "В корзине"
        }}
      </button>
    </div>
  </li>
</template>

<script>
export default {
  props: ["product", "selectedProducts", "loader"],
  computed: {
    isSelected() {
      return this.selectedProducts.some((p) => p.id === this.product.id);
    },
    lastSelected() {
      return (
        this.selectedProducts[this.selectedProducts.length - 1].id ===
        this.product.id
      );
    },
  },
  methods: {
    selectProduct() {
      this.$emit("selectProduct", this.product);
    },

    openModal() {
      this.$emit("openModal", true);
      this.$emit("getDataForModal", this.product);
    },
  },
};
</script>

<style src="./Card.css"></style>
