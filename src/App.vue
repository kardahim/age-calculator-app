<template>
  <div class="card">
    <form class="card__top">
      <Input placeholder="DD" label="day" :value="days" />
      <Input placeholder="MM" label="month" :value="months" />
      <Input placeholder="YYYY" label="year" :value="years" />
      <!-- test:{{ days }} -->
    </form>
    <div class="card__divider">
      <button class="card__divider__button">
        <img src="./assets/images/icon-arrow.svg" alt="arrow icon" />
      </button>
    </div>
    <div class="card__bottom">
      <div class="card__bottom__date">
        <span class="card__bottom__date__number" v-if="errors">--</span>
        <span class="card__bottom__date__number" v-else></span>
        <span class="card__bottom__date__text">years</span>
      </div>
      <div class="card__bottom__date">
        <span class="card__bottom__date__number" v-if="errors">--</span>
        <span class="card__bottom__date__number" v-else></span>
        <span class="card__bottom__date__text">months</span>
      </div>
      <div class="card__bottom__date">
        <span class="card__bottom__date__number" v-if="errors">--</span>
        <span class="card__bottom__date__number" v-else></span>
        <span class="card__bottom__date__text">days</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Input from "./components/Input.vue";

export default defineComponent({
  name: "App",
  components: {
    Input,
  },
  data() {
    return {
      errors: true,
      years: null,
      months: null,
      days: null,
    };
  },
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,700;1,400;1,800&display=swap");
@import "./assets/styles/_variables.scss";

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  min-height: 100vh;
  background-color: $background-color;

  display: flex;
  align-items: center;
  justify-content: center;

  font-family: $ff;

  .card {
    width: 840px;
    height: 650px;
    background-color: $card-color;
    border-radius: 25px;
    border-bottom-right-radius: 200px;
    padding: 55px;

    &__top {
      display: flex;
      justify-content: space-between;
      width: 545px;
    }

    &__divider {
      width: 100%;
      height: 2px;
      background-color: $borders-color;
      margin-top: 50px;
      position: relative;

      &__button {
        width: 96px;
        height: 96px;
        border-radius: 100%;
        border: none;
        outline: none;

        position: absolute;
        right: 0;
        top: -48px;

        background-color: $accent-color;
        transition: background-color 0.3s;

        &:hover {
          cursor: pointer;
          background-color: $date-color;
        }
      }
    }

    &__bottom {
      margin-top: 21px;
      font-size: 105px;
      font-weight: $fw-extra-bold;
      font-style: italic;

      &__date {
        height: 115px;

        span:nth-child(1) {
          color: $accent-color;
          letter-spacing: 15px;
        }

        span:nth-child(2) {
          color: $date-color;
        }
      }
    }
  }
}
</style>
