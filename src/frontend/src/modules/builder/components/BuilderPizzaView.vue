<template>
  <AppDrop @drop="changeIngredientCount">
    <div class="content__pizza">
      <label class="input">
        <span class="visually-hidden">Название пиццы</span>
        <input
          type="text"
          name="pizza_name"
          placeholder="Введите название пиццы"
          :value="value"
          @input="$emit('input', $event.target.value)"
        />
      </label>

      <div class="content__constructor">
        <div class="pizza" :class="foundationClass">
          <div class="pizza__wrapper">
            <div
              v-for="ingredient in pizzaRecipe.ingredients"
              :key="ingredient.id"
            >
              <div
                class="pizza__filling"
                :key="ingredient.id"
                :class="`pizza__filling--${INGREDIENTS_NAMES[ingredient.id]}`"
              ></div>

              <div
                v-if="ingredient.count >= 2"
                class="pizza__filling"
                :class="`pizza__filling--${
                  INGREDIENTS_NAMES[ingredient.id]
                } pizza__filling--second`"
              ></div>

              <div
                v-if="ingredient.count >= 3"
                class="pizza__filling"
                :class="`pizza__filling--${
                  INGREDIENTS_NAMES[ingredient.id]
                } pizza__filling--third`"
              ></div>
            </div>
          </div>
        </div>
      </div>

      <div class="content__result">
        <builder-price-counter :pizza="pizza" :pizza-recipe="pizzaRecipe" />
        <button type="button" class="button" :disabled="isNotReady">
          Готовьте!
        </button>
      </div>
    </div>
  </AppDrop>
</template>

<script>
import {
  DOUGH_TYPES,
  SAUCES_NAMES,
  INGREDIENTS_NAMES,
  PIZZA_SIZES,
} from "@/common/constants";

import BuilderPriceCounter from "@/modules/builder/components/BuilderPriceCounter";
import AppDrop from "@/common/components/AppDrop";

export default {
  name: "BuilderPizzaView",
  components: {
    BuilderPriceCounter,
    AppDrop,
  },
  props: {
    pizza: {
      type: Object,
      required: true,
    },
    pizzaRecipe: {
      type: Object,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      DOUGH_TYPES,
      SAUCES_NAMES,
      INGREDIENTS_NAMES,
      PIZZA_SIZES,
    };
  },
  computed: {
    foundationClass() {
      const doughClass = this.pizzaRecipe.dough.id === 1 ? "small" : "big";
      const sauceClass = this.SAUCES_NAMES[this.pizzaRecipe.sauces.id];
      return `pizza--foundation--${doughClass}-${sauceClass}`;
    },
    computedIngredients() {
      const computedIngredients = [];

      this.pizzaRecipe.ingredients.forEach((ingredient) => {
        computedIngredients.push({
          id: ingredient.id,
          class: "",
        });

        if (ingredient.count === 2) {
          computedIngredients.push({
            id: ingredient.id,
            class: "pizza__filling--second",
          });
        } else if (ingredient.count === 3) {
          computedIngredients.push({
            id: ingredient.id,
            class: "pizza__filling--third",
          });
        }
      });

      return computedIngredients;
    },
    isNotReady() {
      return !this.value.length || !this.pizzaRecipe.ingredients.length;
    },
  },
  methods: {
    changeIngredientCount({ id }) {
      this.$emit("pizza-param-changed", {
        pizzaParam: "ingredients",
        id,
        count: 1,
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
