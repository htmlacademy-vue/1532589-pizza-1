<template>
  <div class="content__ingredients">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите ингредиенты</h2>

      <div class="sheet__content ingredients">
        <div class="ingredients__sauce">
          <p>Основной соус:</p>
          <radio-button
            class="radio ingredients__input"
            v-for="sauce in pizza.sauces"
            :key="sauce.id"
            :value="sauce.id"
            :inputName="'sauce'"
            :isChecked="pizzaRecipe.sauces.id === sauce.id"
            @change="
              $emit('pizza-param-changed', {
                pizzaParam: 'sauces',
                id: $event.target.value,
              })
            "
          >
            <span>{{ sauce.name }}</span>
          </radio-button>
        </div>

        <div class="ingredients__filling">
          <p>Начинка:</p>

          <ul class="ingredients__list">
            <li
              v-for="ingredient in pizza.ingredients"
              :key="ingredient.id"
              class="ingredients__item"
            >
              <AppDrag
                :transfer-data="ingredient"
                :draggable="canBeDragged(ingredient)"
              >
                <SelectorItem
                  :ingredient="ingredient"
                  :pizzaRecipe="pizzaRecipe"
                  @change-ingredient-count="changeIngredientCount"
                />
              </AppDrag>
              <item-counter
                :ingredientId="ingredient.id"
                :pizzaRecipe="pizzaRecipe"
                @change-ingredient-count="changeIngredientCount"
              />
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { SAUCES_NAMES, INGREDIENTS_NAMES } from "@/common/constants";

import ItemCounter from "@/common/components/ItemCounter";
import RadioButton from "@/common/components/RadioButton";
import SelectorItem from "@/common/components/SelectorItem";
import AppDrag from "@/common/components/AppDrag";

export default {
  name: "BuilderIngredientsSelector",
  components: {
    ItemCounter,
    RadioButton,
    SelectorItem,
    AppDrag,
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
  },
  data() {
    return {
      SAUCES_NAMES,
      INGREDIENTS_NAMES,
    };
  },
  methods: {
    changeIngredientCount({ id, count }) {
      this.$emit("pizza-param-changed", {
        pizzaParam: "ingredients",
        id,
        count,
      });
    },
    canBeDragged({ id }) {
      const isInRecipe = this.pizzaRecipe.ingredients.some(
        (ing) => ing.id === id
      );
      const foundIngredient = this.pizzaRecipe.ingredients.find(
        (ing) => ing.id === id
      );

      if (foundIngredient) {
        const isMaxRecipes = foundIngredient.count === 3;
        return !(isInRecipe && isMaxRecipes);
      }
      return !isInRecipe;
    },
  },
};
</script>

<style lang="scss" scoped></style>
