<template>
  <div class="card">
    <form @submit.prevent="onSubmit">
      <div class="card__top">
        <Input placeholder="DD" label="day" v-model="daysInput" />
        <Input placeholder="MM" label="month" v-model="monthsInput" />
        <Input placeholder="YYYY" label="year" v-model="yearsInput" />
      </div>
      <div class="card__divider">
        <button class="card__divider__button" type="submit">
          <img src="./assets/images/icon-arrow.svg" alt="arrow icon" />
        </button>
      </div>
    </form>
    <div class="card__bottom">
      <div class="card__bottom__date">
        <span class="card__bottom__date__number" v-if="errors || firstLoad"
          >--</span
        >
        <span class="card__bottom__date__number" v-else>{{ years }}</span>
        <span class="card__bottom__date__text">years</span>
      </div>
      <div class="card__bottom__date">
        <span class="card__bottom__date__number" v-if="errors || firstLoad"
          >--</span
        >
        <span class="card__bottom__date__number" v-else>{{ months }}</span>
        <span class="card__bottom__date__text">months</span>
      </div>
      <div class="card__bottom__date">
        <span class="card__bottom__date__number" v-if="errors || firstLoad"
          >--</span
        >
        <span class="card__bottom__date__number" v-else>{{ days }}</span>
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
      firstLoad: true,
      errors: false,
      yearsInput: null,
      monthsInput: null,
      daysInput: null,
      years: "",
      months: "",
      days: "",
      yearsError: "",
      monthsError: "",
      daysError: "",
      dataRegex:
        /^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1|(?:(?:29|30)(\/|-|\.)(?:0?[13-9]|1[0-2])\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9])|(?:1[0-2]))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$/,
    };
  },
  methods: {
    onSubmit() {
      this.firstLoad = false;

      // fields are required
      if (!this.yearsInput || !this.monthsInput || !this.daysInput) {
        this.errors = true;

        if (!this.yearsInput) this.yearsError = "The field is required";

        if (!this.monthsInput) this.monthsError = "The field is required";

        if (!this.daysInput) this.daysError = "The field is required";
      }
      // validate date
      else if (
        !this.dataRegex.test(
          `${this.daysInput}.${this.monthsInput}.${this.yearsInput}`
        )
      ) {
        this.errors = true;
        this.daysError = "Must be a valid";
        this.monthsError = "";
        this.yearsError = "";
      }
      // correct date
      else {
        this.errors = false;
        this.yearsError = "";
        this.monthsError = "";
        this.daysError = "";

        // calculate time difeerence
        let beginDate: Date = new Date(
          `${this.yearsInput}-${this.monthsInput}-${this.daysInput}`
        );
        let endDate: Date = new Date();
        let timeDifference: number = endDate.getTime() - beginDate.getTime();

        // milliseconds in one day, month, year
        let dayMilliseconds: number = 1000 * 60 * 60 * 24;
        let monthMilliseconds: number = dayMilliseconds * 30.44; // average day in month
        let yearMilliseconds: number = dayMilliseconds * 365.25; // average day in year

        let timeLeft = 0;
        this.years = String(Math.floor(timeDifference / yearMilliseconds));
        timeLeft = timeDifference % yearMilliseconds;
        this.months = String(Math.floor(timeLeft / monthMilliseconds));
        timeLeft = timeLeft % monthMilliseconds;
        this.days = String(Math.floor(timeLeft / dayMilliseconds));
      }
    },
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
