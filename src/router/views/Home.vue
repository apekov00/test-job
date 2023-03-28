<template>
  <section>
    <div class="wrapper">
      <div class="left-bar">
        <MenuBurger />

        <div class="left-bar__slide">
          <div
            class="left-bar__line"
            v-for="slide in slides"
            :key="slide.id"
            @click="showCurrentSlideById(slide.id)"
          >
            <template v-if="slide.id === activeSlideId">
              <p class="left-bar__number-slide animate__animated animate__flipInX">0{{ slide.id }}</p>
              <p class="left-bar__txt-slide animate__animated animate__flipInX">
                {{ slide.desc }}
              </p>
              <span class="line animate__animated animate__flipInX" />
            </template>
            <span v-else class="line short-line" />
          </div>
        </div>

        <div class="left-bar__down-arrow">
          <p class="left-bar__arrow-txt">Скрольте вниз</p>
          <span class="left-bar__arrow">
            <img src="@/assets/images/icon/down.svg" alt="" />
          </span>
        </div>
      </div>

      <div class="main">
        <div class="main__bg">
          <img
            class="main__logo"
            src="@/assets/images/icon/kinopoisk.svg"
            alt=""
          />
          <h1 class="txt-h1 mrg-b-t">ОНИ ДОЛЖНЫ ЧТО-ТО ЗНАТЬ</h1>
          <div class="main__circle">
            {{ activeSlideId }}/{{ slides.length }}
          </div>
          <button class="main__btn btn">Искать промокод <img class="main__arrow-btn" src="@/assets/images/icon/right.svg" alt=""></button>
          <div class="main__right-txt">hd.kinopoisk.ru</div>
        </div>

        <div
          v-for="slide in slides"
          :key="slide.text"
          :class="{
            hidden: slide.id !== activeSlideId,
            main__slide: true,
          }"
        >
          <img
            :class="`main__slide-img1 animate__animated animate__slideIn${slideDirection}`"
            :src="slide.image"
            alt=""
          />
          <p class="main__slide-txt txt-p">
            {{ slide.text }}
          </p>
        </div>

        <div class="arrows">
          <div class="arrow" @click="handleShowPrevSlide">
            <img src="@/assets/images/icon/left-arrow.svg" alt="" />
          </div>
          <div class="arrow" @click="handleShowNextSlide">
            <img src="@/assets/images/icon/right-arrow.svg" alt="" />
          </div>
        </div>

        <div class="main__bg-cloud">
          <img class="main__cloud" src="@/assets/images/cloud.png" alt="" />
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import { ref } from "vue";
import MenuBurger from "../../components/MenuBurger.vue";
import slide1 from "@/assets/images/slide1.png";
import slide2 from "@/assets/images/slide2.png";
import slide3 from "@/assets/images/slide3.png";
import slide4 from "@/assets/images/slide4.png";

const slides = [
  {
    id: 1,
    text: "Для примера мы показали вам его лицо. В первой серии он прячется в подвале за мониторами, и пусть борода не собьёт вас с толку. Найдите героя и нажмите на паузу — ему не терпится отдать вам промокод.",
    desc: "У Бога новый проект",
    image: slide1,
  },
  {
    id: 2,
    text: "some text 2",
    desc: "Всем привет",
    image: slide2,
  },
  {
    id: 3,
    text: "some text 3",
    desc: "Подсказка",
    image: slide3,
  },
  {
    id: 4,
    text: "some text 4",
    desc: "Вопросы и ответы",
    image: slide4,
  },
];
export default {
  name: "Home",
  components: { MenuBurger },
  setup() {
    const activeSlideId = ref(1);
    const slideDirection = ref("Right");

    const handleShowNextSlide = () => {
      slideDirection.value = "Right";
      if (activeSlideId.value === slides.length) {
        activeSlideId.value = 1;
      } else {
        activeSlideId.value = activeSlideId.value + 1;
      }
    };

    const handleShowPrevSlide = () => {
      slideDirection.value = "Left";
      if (activeSlideId.value === 1) {
        activeSlideId.value = slides.length;
      } else {
        activeSlideId.value = activeSlideId.value - 1;
      }
    };

    const showCurrentSlideById = (id) => {
      if (id < activeSlideId.value) {
        slideDirection.value = "Left";
      } else {
        slideDirection.value = "Right";
      }
      activeSlideId.value = id;
    };

    return {
      activeSlideId,
      slideDirection,
      handleShowNextSlide,
      handleShowPrevSlide,
      showCurrentSlideById,
      slides,
    };
  },
};
</script>
<style>
@import "../../styles.css";
</style>
