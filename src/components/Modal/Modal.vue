<template>
  <div
    class="modal"
    v-bind:class="{ modal_active: modalState }"
    @click="closeModal"
  >
    <div class="modal__container">
      <div class="slider">
        <div class="slider__container">
          <SliderImage
            v-for="(image, i) of modalData.images"
            v-bind:key="i"
            v-bind:image="image"
          />
        </div>
      </div>
      <div class="slider__buttons">
        <div
          @click="handleSliderBtnLeft"
          class="slider__btn slider__btn_left"
        ></div>
        <div
          @click="handleSliderBtnRight"
          class="slider__btn slider__btn_right"
        ></div>
      </div>
      <h2 class="modal__title">{{ modalData.title }}</h2>
      <p class="modal__description">{{ modalData.description }}</p>
      <p class="modal__cost">{{ modalData.cost }}</p>
    </div>
  </div>
</template>

<script>
import SliderImage from "../SliderImage/SliderImage.vue";

export default {
  props: ["modalState", "modalData"],
  components: {
    SliderImage,
  },
  data() {
    return {
      count: 0,
      position: 0,
    };
  },
  methods: {
    closeModal(e) {
      this.$emit("closeModal", e);
    },

    handleSliderBtnRight() {
      const container = document.querySelector(".slider__container");
      if (this.count <= this.modalData.images.length - 2) {
        ++this.count;
      }
      container.style.marginLeft = this.count * -550 + "px";
    },

    handleSliderBtnLeft() {
      const container = document.querySelector(".slider__container");

      if (this.count > 0) {
        --this.count;
      }

      container.style.marginLeft = this.count * -550 + "px";
    },
  },
};
</script>

<style src="./Modal.css"></style>
