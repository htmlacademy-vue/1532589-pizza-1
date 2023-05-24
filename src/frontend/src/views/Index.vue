<template>
  <body>
    <header class="header">
      <div class="header__logo">
        <a href="index.html" class="logo">
          <img
            src="img/logo.svg"
            alt="V!U!E! Pizza logo"
            width="90"
            height="40"
          />
        </a>
      </div>
      <div class="header__cart">
        <a href="cart.html">0 ₽</a>
      </div>
      <div class="header__user">
        <a href="#" class="header__login"><span>Войти</span></a>
      </div>
    </header>

    <main class="content">
      <form action="#" method="post">
        <div class="content__wrapper">
          <h1 class="title title--big">Конструктор пиццы</h1>

          <builder-dough-selector
            :pizza="pizza"
            :pizza-recipe="pizzaRecipe"
            @pizza-param-changed="changeRecipe"
          />

          <builder-size-selector
            :pizza="pizza"
            :pizza-recipe="pizzaRecipe"
            @pizza-param-changed="changeRecipe"
          />

          <builder-ingredients-selector
            :pizza="pizza"
            :pizza-recipe="pizzaRecipe"
            @pizza-param-changed="changeRecipe"
          />

          <builder-pizza-view
            :pizza="pizza"
            :pizza-recipe="pizzaRecipe"
            @pizza-param-changed="changeRecipe"
            v-model="pizzaName"
          />
        </div>
      </form>
    </main>
  </body>
</template>

<script>
import misc from "@/static/misc.json";
import pizza from "@/static/pizza.json";
import user from "@/static/user.json";

import {
  DOUGH_TYPES,
  PIZZA_SIZES,
  SAUCES_NAMES,
  INGREDIENTS_NAMES,
} from "@/common/constants";

import BuilderDoughSelector from "@/modules/builder/components/BuilderDoughSelector";
import BuilderSizeSelector from "@/modules/builder/components/BuilderSizeSelector";
import BuilderIngredientsSelector from "@/modules/builder/components/BuilderIngredientsSelector";
import BuilderPizzaView from "@/modules/builder/components/BuilderPizzaView";

export default {
  name: "Views",
  components: {
    BuilderDoughSelector,
    BuilderSizeSelector,
    BuilderIngredientsSelector,
    BuilderPizzaView,
  },
  data() {
    return {
      misc,
      pizza,
      user,

      DOUGH_TYPES,
      PIZZA_SIZES,
      SAUCES_NAMES,
      INGREDIENTS_NAMES,

      pizzaRecipe: {
        dough: { ...pizza.dough[0] },
        sizes: { ...pizza.sizes[0] },
        sauces: { ...pizza.sauces[0] },
        ingredients: [],
      },
      pizzaName: "",
    };
  },
  methods: {
    changeRecipe(obj) {
      if (obj.pizzaParam === "ingredients") {
        this.setRecipeIngredient(obj);
      } else {
        this.setRecipeParam(obj);
      }
    },
    setRecipeParam({ pizzaParam, id }) {
      this.pizzaRecipe[pizzaParam] = {
        ...this.pizza[pizzaParam].find((param) => param.id === +id),
      };
    },
    setRecipeIngredient({ pizzaParam, id, count }) {
      const itemIndex = this.pizzaRecipe[pizzaParam].findIndex(
        (item) => item.id === id
      );
      if (~itemIndex) {
        const ingredient = this.pizzaRecipe[pizzaParam][itemIndex];
        const ingredientNewCount = ingredient.count + count;
        if (ingredientNewCount === 0) {
          this.pizzaRecipe[pizzaParam].splice(itemIndex, 1);
        } else {
          ingredient.count = ingredientNewCount;
        }
      } else {
        this.pizzaRecipe[pizzaParam].push({
          ...(this.pizza[pizzaParam].filter((ing) => ing.id === id)[0] || []),
          count,
        });
      }
    },
  },
};
</script>

<style></style>
