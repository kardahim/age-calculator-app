<template>
  <div class="input">
    <label :for="label">{{ label }}</label>
    <input type="text" :id="label" :placeholder="placeholder" :name="label" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Input",
  props: {
    placeholder: String,
    label: String,
    value: Number,
  },
});
</script>

<style scoped lang="scss">
@import "../assets/styles/_variables.scss";

.input {
  width: 160px;
  color: $input-color;
  font-family: $ff;

  display: flex;
  flex-direction: column;

  label {
    text-transform: uppercase;
    font-weight: $fw-bold;
    font-size: 14px;
    letter-spacing: 4px;
    margin-bottom: 10px;
    font-family: $ff;
  }
  input {
    height: 70px;
    width: 100%;
    text-indent: 22px;
    font-size: $fs-inputs;
    font-weight: $fw-bold;
    font-family: $ff;
    cursor: pointer;
    outline: none;
    border: 1px solid $borders-color;
    border-radius: 5px;

    &:active,
    &:focus {
      border: 1px solid $accent-color;
    }
  }
}
</style>
