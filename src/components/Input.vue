<template>
  <div class="input">
    <label :for="label" :class="hasError && 'label-error'">{{ label }}</label>
    <input
      :class="hasError && 'input-error'"
      type="text"
      :id="label"
      :placeholder="placeholder"
      :name="label"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
    <span v-if="hasError" class="error-message">{{ errorMessage }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Input",
  emits: ["update:modelValue"],
  props: {
    modelValue: String,
    placeholder: String,
    label: String,
    hasError: Boolean,
    errorMessage: String,
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
  .label-error {
    color: $errors-color;
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

  .input-error {
    border: 1px solid $errors-color;
  }

  .error-message {
    color: $errors-color;
    font-weight: $fw-regular;
    font-size: 14px;
    margin-top: 10px;
    font-style: italic;
  }
}
</style>
