<template>
  <div class="content__dough">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите тесто</h2>

      <div class="sheet__content dough">
        <radio-button
          class="dough__input"
          v-for="dough in pizza.dough"
          :key="dough.id"
          :value="dough.id"
          :inputName="'dough'"
          :isChecked="pizzaRecipe.dough.id === dough.id"
          :class="`dough__input--${DOUGH_TYPES[dough.id]}`"
          @change="
            $emit('pizza-param-changed', {
              pizzaParam: 'dough',
              id: $event.target.value,
            })
          "
        >
          <b>{{ dough.name }}</b>
          <span>{{ dough.description }}</span>
        </radio-button>
      </div>
    </div>
  </div>
</template>

<script>
import { DOUGH_TYPES } from "@/common/constants";

import RadioButton from "@/common/components/RadioButton";

export default {
  name: "BuilderDoughSelector",
  components: {
    RadioButton,
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
      DOUGH_TYPES,
    };
  },
};
</script>

<style lang="scss" scoped></style>
