<template>
  <label>
    <input
      type="radio"
      class="visually-hidden"
      :checked="isChecked"
      :value="value"
      :name="inputName"
      v-on="$listeners"
    />
    <slot />
  </label>
</template>

<script>
export default {
  name: "RadioButton",
  props: {
    value: {
      type: Number,
      required: true,
    },
    inputName: {
      type: [String],
      required: true,
    },
    isChecked: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped></style>
