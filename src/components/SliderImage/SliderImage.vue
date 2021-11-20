<template>
  <div class="slider__image-containder">
    <img :src="image" class="slider__image" alt="постер" />
  </div>
</template>

<script>
export default {
  props: ["image"],
};
</script>

<style src="./SliderImage.css"></style>
