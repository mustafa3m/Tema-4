<template>
  <div class="slider">
    <button @click="prev" type="button" class="slider__buttton slider__buttton__left">←</button>
    <div
      class="slider__container"
      :style="{
        transform: ` translateX(${index}%)`,
        transition: `${transition}`,
      }"
    >
      <img
        class="slider__img"
        v-for="(slide, index) in slides"
        :key="index"
        :src="slide"
        :alt="slide"
      />
    </div>

    <button @click="next" class="slider__buttton slider__buttton__right">→</button>
  </div>
</template>

;

<script>
  export default {
    name: "Slider",

    data() {
      return {
        index: 0,

        slides: [
          "https://images.unsplash.com/photo-1590634875887-a6a516622e2a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1352&q=80",
          "https://images.unsplash.com/photo-1590664216212-62e763768cae?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80",
          "https://images.unsplash.com/photo-1559467713-f830ec30e3e4?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80",
        ],

        transition: "transform 0.2s ease",
      };
    },

    methods: {
      /* two methods, "next" and "prev", to control the transition and index of an element */

      
      next() {
        if (this.index === -200) {
          this.transition = "none";

          this.index = 0;
        } else {
          this.transition = "transform 0.2s ease";

          this.index -= 100;
        }
      },

      

      prev() {
        if (this.index === 0) {
          this.transition = "none";

          this.index = -200;
        } else {
          this.transition = "transform 0.2s ease";

          this.index += 100;
        }
      },
    },
  };
</script>

<style scoped>
  .slider {
    width: 100%;
    height: 500px;
    margin: 100px auto 0;
    overflow: hidden;
    position: relative;
  }

  .slider__container {
    display: flex;
  }

  .slider__img {
    min-width: 100%;
    max-width: 100%;
    height: 100%;
  }

  .slider__buttton {
    outline: none;
    border: none;
    width: 90px;
    height: 50px;
    border-radius: 50%;
    display: block;
    position: absolute;
    z-index: 1000;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    color: red;
    font-size: 70px;
  }

  .slider__buttton__left {
    top: 50%;
    left: 5px;
    transform: translateY(-50%);
  }

  .slider__buttton__right {
    top: 50%;
    right: 5px;
    transform: translateY(-50%);
  }
</style>
