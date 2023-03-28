<template>
  <div class="burger">
    <div class="burger__container">
      <button class="burger__btn" id="burger">
        <span class="span"></span>
        <span class="span"></span>
        <span class="span"></span>
      </button>
      <nav class="menu">
        <ul class="menu__list">
          <li class="menu__item">
            <a href="#" class="menu__link">пункт 1</a>
          </li>
          <li class="menu__item">
            <a href="#" class="menu__link">пункт 2</a>
          </li>
          <li class="menu__item">
            <a href="#" class="menu__link">пункт 3</a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import { onMounted } from "vue";

export default {
  name: "MenuBurger",
  setup() {
    onMounted(() => {
      document.getElementById("burger").addEventListener("click", function () {
        document.querySelector(".burger").classList.toggle("open");
      });
    });
  },
};
</script>
