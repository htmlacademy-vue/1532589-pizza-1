<template>
  <div class="counter ingredients__counter">
    <button
      type="button"
      class="counter__button counter__button--minus"
      :disabled="decDisabled"
      @click="$emit('change-ingredient-count', { id: ingredientId, count: -1 })"
    >
      <span class="visually-hidden">Меньше</span>
    </button>

    <input
      type="text"
      name="counter"
      class="counter__input"
      :value="CurrentValue"
      readonly
    />

    <button
      type="button"
      class="counter__button counter__button--plus"
      :disabled="incDisabled"
      @click="$emit('change-ingredient-count', { id: ingredientId, count: 1 })"
    >
      <span class="visually-hidden">Больше</span>
    </button>
  </div>
</template>

<script>
import { MIN_COUNTER_VALUE, MAX_COUNTER_VALUE } from "@/common/constants";

export default {
  name: "ItemCounter",
  props: {
    value: {
      type: Number,
      default: 0,
    },
    ingredientId: {
      type: Number,
      required: true,
    },
    pizzaRecipe: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {};
  },
  computed: {
    CurrentValue() {
      return (
        this.pizzaRecipe.ingredients.filter(
          (ing) => ing.id === this.ingredientId
        )[0]?.count ?? MIN_COUNTER_VALUE
      );
    },

    incDisabled() {
      return (
        this.pizzaRecipe.ingredients.filter(
          (ing) => ing.id === this.ingredientId
        )[0]?.count === MAX_COUNTER_VALUE
      );
    },
    decDisabled() {
      return !this.pizzaRecipe.ingredients.find(
        (ing) => ing.id === this.ingredientId
      );
    },
  },
};
</script>

<style lang="scss" scoped></style>
