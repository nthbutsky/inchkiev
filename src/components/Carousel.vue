<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />

    <!-- navigation button -->
    <div class="carousel__btn" @click="nextSlide">
      <svg viewBox="0 0 100 100" width="100" height="100">
        <defs>
          <path
            id="circle"
            d="
        M 50, 50
        m -37, 0
        a 37,37 0 1,1 74,0
        a 37,37 0 1,1 -74,0"
          />
        </defs>
        <text font-size="10">
          <textPath xlink:href="#circle">
            дивитися далі - дивитися далі - дивитися далі -
          </textPath>
        </text>
      </svg>
      <span>&#8594;</span>
    </div>

    <!-- pagination -->
    <div class="carousel__pagination">
      <span>{{ currentSlide }}/{{ slideCount }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "carousel",

  data() {
    return {
      currentSlide: 1,
      slideCount: null,
      slideAutoplay: true,
      timeout: 5000,
    };
  },

  methods: {
    nextSlide() {
      if (this.currentSlide === this.slideCount) {
        this.currentSlide = 1;
        return;
      }
      this.currentSlide += 1;
    },

    autoplay() {
      setInterval(() => {
        this.nextSlide();
      }, this.timeout);
    },
  },

  mounted() {
    this.slideCount = document.querySelectorAll(".slide").length;
    if (this.slideAutoplay) {
      this.autoplay();
    }
  },
};
</script>

<style scoped lang="scss">
.carousel {
  &__btn {
    position: absolute;
    top: 18rem;
    left: 87rem;
    transform: translate(-50%);
    cursor: pointer;

    svg {
      fill: white;
      height: auto;
      transform-origin: center;
      width: 7rem;
      animation: rotation infinite 6s linear;

      @keyframes rotation {
        0% {
          transform: rotate(0deg);
        }
        100% {
          transform: rotate(360deg);
        }
      }
    }

    span {
      position: absolute;
      top: 40%;
      left: 50%;
      transform: translate(-50%, -40%);
      font-size: 40px;
      color: white;
    }
  }

  &__pagination {
    position: absolute;
    bottom: 3rem;
    left: 15rem;
    height: 60px;
    width: 120px;
    border-radius: 50%;
    border: 2px solid white;

    span {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      color: white;
    }
  }
}
</style>
