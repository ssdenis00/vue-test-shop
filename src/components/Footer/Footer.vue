<template>
  <footer class="footer">
    <Menu />
    <div class="footer__contacts">
      <a href="tel:+78125555555" class="footer__link"
        ><img
          src="../../images/footer-phone-icon.svg"
          alt="иконка телефона"
          class="footer__icon"
        />
        +7 (812) 555-55-55</a
      >
      <a href="" class="footer__link"
        ><img
          src="../../images/footer-location-icon.svg"
          alt="иконка локации"
          class="footer__icon"
        />
        г. Санкт-Петербург, ул. Ефимова, 3</a
      >
    </div>
  </footer>
</template>

<script>
import Menu from "../Menu/Menu.vue";

export default {
  name: "Footer",
  components: { Menu },
};
</script>

<style src="./Footer.css"></style>
