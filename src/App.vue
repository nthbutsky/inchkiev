<template>
  <div id="app">
    <Carousel class="carousel" v-slot="{ currentSlide }">
      <Slide v-for="(slide, index) in carouselSlides" :key="index">
        <div
          class="slide-info"
          v-show="currentSlide === index + 1"
          :style="{
            background: slide.color,
          }"
        >
          <div class="slide-info__left-side-wrapper">
            <div class="slide-info__oval-four"></div>
            <img
              class="slide-info__star-thing"
              :src="require(`./assets/star.svg`)"
              alt="Star"
            />
            <p class="slide-info__top-text">lorem ipsum dolor, sit amet</p>
            <p class="slide-info__text-line-one">lorem ipsum</p>
            <p class="slide-info__text-line-two">lorem ipsum dolor -</p>
            <p class="slide-info__text-line-three">lorem</p>
            <p class="slide-info__text-line-four">ipsum!</p>
            <p class="slide-info__bottom-text">
              lorem ipsum dolor sit, amet consectetur adipisicing elit
            </p>
          </div>
          <div class="slide-info__right-side-wrapper">
            <div class="slide-info__oval-one"></div>
            <div class="slide-info__oval-two"></div>
            <div class="slide-info__oval-three">
              <img :src="require(`./assets/dog.jpg`)" alt="Dog" />
            </div>
          </div>
        </div>
      </Slide>
    </Carousel>
    <Form />
    <Movies />
  </div>
</template>

<script>
import Carousel from "./components/Carousel.vue";
import Slide from "./components/Slide.vue";
import Form from "./components/Form.vue";
import Movies from "./components/Movies.vue";

export default {
  components: {
    Carousel,
    Slide,
    Form,
    Movies,
  },

  data() {
    return {
      carouselSlides: [
        { color: "#027d84" },
        { color: "#4a989a" },
        { color: "#a1a1a1" },
      ],
    };
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -ms-overflow-style: none;
  scrollbar-width: none;

  &::-webkit-scrollbar {
    display: none;
  }
}

#app {
  font-family: Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  cursor: default;
}

.carousel {
  position: relative;
  max-height: 700px;
  height: 100vh;
}

.slide-info {
  position: absolute;
  top: 0;
  left: 0;
  max-height: 100%;
  height: 100%;
  width: 100%;
  border-top-right-radius: 5.625rem;
  border-bottom-right-radius: 5.625rem;
  color: white;
  text-transform: uppercase;
  display: flex;
  flex-direction: row;
  justify-content: space-around;

  &__right-side-wrapper {
    position: relative;
    z-index: 1;
    max-height: 700px;
  }

  &__left-side-wrapper {
    position: relative;
    z-index: 2;
    max-height: 700px;
  }

  &__oval-one {
    position: absolute;
    bottom: 3rem;
    right: 16rem;
    display: inline-block;
    height: 27.5rem;
    width: 13.4375rem;
    border-radius: 50%;
    background: #afb3b4;
    transform: rotate(75deg);
  }

  &__oval-two {
    position: absolute;
    bottom: 12rem;
    right: 14rem;
    display: inline-block;
    height: 27.5rem;
    width: 13.4375rem;
    border-radius: 50%;
    border: 2px solid white;
    transform: rotate(130deg);
  }

  &__oval-three {
    position: absolute;
    bottom: 3rem;
    right: 25rem;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 27.5rem;
    width: 13.4375rem;
    border-radius: 50%;
    overflow: hidden;
    transform: rotate(55deg);

    img {
      transform: rotate(-55deg);
    }
  }

  &__oval-four {
    position: absolute;
    top: -16rem;
    left: 15rem;
    display: inline-block;
    height: 27.5rem;
    width: 13.4375rem;
    border-radius: 50%;
    background: #afb3b4;
    transform: rotate(100deg);
  }

  &__star-thing {
    position: absolute;
    top: 25rem;
    left: 0;
    animation: pulse infinite alternate 2s ease-in-out;

    @keyframes pulse {
      0% {
        transform: scale(1);
      }
      100% {
        transform: scale(0.9);
      }
    }

    &:hover {
      animation: rotate 1s ease-in-out;

      @keyframes rotate {
        0% {
          transform: rotate(0deg);
        }
        100% {
          transform: rotate(360deg);
        }
      }
    }
  }

  &__top-text {
    position: absolute;
    top: 1rem;
    left: 14rem;
    font-weight: normal;
    font-size: 1.125rem;
    text-shadow: 4px 4px 4px rgba(0, 0, 0, 0.25);
  }

  &__text-line-one {
    font-size: 3.75rem;
    font-weight: bold;
    padding: 6.25rem 0 0 9.375rem;
  }

  &__text-line-two {
    font-size: 3.75rem;
    font-weight: normal;
    padding: 0 0 0 11.875rem;
  }

  &__text-line-three {
    font-size: 3.75rem;
    font-weight: normal;
    padding: 0 0 0 27.5rem;
  }

  &__text-line-four {
    font-size: 3.75rem;
    font-weight: normal;
    padding: 0 0 0 18.75rem;
  }

  &__bottom-text {
    font-weight: normal;
    font-size: 0.9375rem;
    width: 43.75rem;
    line-height: 1.375rem;
    padding: 3.125rem 0 0 28.125rem;
  }

  @media (max-width: 1440px) {
    .slide-info__oval-one,
    .slide-info__oval-two,
    .slide-info__oval-three {
      height: 300px;
      width: 170px;
    }

    .slide-info__oval-three img {
      height: 80%;
    }

    .slide-info__text-line-one,
    .slide-info__text-line-two,
    .slide-info__text-line-tree {
      font-size: 3rem;
    }
  }
}
</style>
