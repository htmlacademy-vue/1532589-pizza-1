<template>
  <span :class="`filling--${INGREDIENTS_NAMES[ingredient.id]}`" class="filling">
    {{ ingredient.name }}
  </span>
</template>

<script>
import { INGREDIENTS_NAMES } from "@/common/constants";

export default {
  name: "SelectorItem",
  props: {
    ingredient: {
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
      INGREDIENTS_NAMES,
    };
  },
};
</script>
