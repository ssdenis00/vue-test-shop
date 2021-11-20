<template>
  <div class="app">
    <Header v-on:getInputValue="searchProduct" />
    <Modal
      v-bind:modalState="modalState"
      @closeModal="closeModal"
      v-bind:modalData="modalData"
    />
    <Main
      v-bind:products="products"
      @selectProduct="selectProduct"
      v-bind:selectedProducts="selectedProducts"
      v-bind:loader="loader"
      @getDataForModal="getDataForModal"
      @openModal="openModal"
    />
    <Footer />
  </div>
</template>

<script>
import Header from "../Header/Header.vue";
import Footer from "../Footer/Footer.vue";
import Main from "../Main/Main.vue";
import Modal from "../Modal/Modal.vue";
import venereImage from "../../images/venere.png";
import daVinciImage from "../../images/da-vinci.png";
import mikelangelo from "../../images/mikelangelo.png";
import rembrant from "../../images/rembrant.png";

export default {
  name: "App",
  data() {
    return {
      products: [
        {
          id: 1,
          title: "«Рождение Венеры» Сандро Боттичелли",
          description: "Описание краткое",
          cost: "1 000 000 $",
          lastCost: "2 000 000 $",
          available: true,
          images: [venereImage, daVinciImage, mikelangelo, rembrant],
        },
        {
          id: 2,
          title: "«Тайная вечеря»  Леонардо да Винчи",
          description: "Описание краткое",
          cost: "3 000 000 $",
          lastCost: "",
          available: true,
          images: [daVinciImage, venereImage, mikelangelo, rembrant],
        },
        {
          id: 3,
          title: "«Сотворение Адама» Микеланджело",
          description: "Описание краткое",
          cost: "5 000 000 $",
          lastCost: "6 000 000 $",
          available: true,
          images: [mikelangelo, venereImage, daVinciImage, rembrant],
        },
        {
          id: 4,
          title: "«Урок анатомии»  Рембрандт",
          description: "Описание краткое",
          cost: "5 000 000 $",
          lastCost: "6 000 000 $",
          available: false,
          images: [rembrant, venereImage, daVinciImage, mikelangelo],
        },
      ],
      defaultProducts: [],
      selectedProducts: [],
      loader: false,
      modalState: false,
      modalData: {},
    };
  },
  components: {
    Header,
    Footer,
    Main,
    Modal,
  },
  mounted() {
    localStorage.getItem("selectedProducts")
      ? (this.selectedProducts = JSON.parse(
          localStorage.getItem("selectedProducts")
        ))
      : (this.selectedProducts = []);

    this.defaultProducts = JSON.parse(JSON.stringify(this.products));
  },
  methods: {
    getDataForModal(data) {
      this.modalData = data;
    },

    openModal() {
      this.modalState = true;
    },

    closeModal(e) {
      if (e.target === e.currentTarget) this.modalState = false;
    },

    searchProduct(inputValue) {
      inputValue.trim() === ""
        ? (this.products = this.defaultProducts)
        : (this.products = this.defaultProducts.filter((item) => {
            const transformTitle = item.title.toLowerCase();
            const transformInputValue = inputValue.toLowerCase();

            return transformTitle.includes(transformInputValue);
          }));
    },

    selectProduct(res) {
      this.loader = true;

      this.selectedProducts.some((p) => p.id === res.id)
        ? this.selectedProducts
        : (this.selectedProducts = [...this.selectedProducts, res]);

      localStorage.setItem(
        "selectedProducts",
        JSON.stringify(this.selectedProducts)
      );

      setTimeout(() => {
        this.loader = false;
      }, 2000);
    },
  },
};
</script>

<style src="./App.css"></style>
