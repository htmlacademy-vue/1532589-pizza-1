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

          <div class="content__dough">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите тесто</h2>

              <div class="sheet__content dough">
                <label
                  v-for="dough in pizza.dough"
                  :key="dough.id"
                  class="dough__input"
                  :class="{
                    'dough__input--light': dough.name === 'Тонкое',
                    'dough__input--large': dough.name === 'Толстое',
                  }"
                >
                  <input
                    type="radio"
                    name="dought"
                    value="light"
                    class="visually-hidden"
                    checked
                  />
                  <b>{{ dough.name }}</b>
                  <span>{{ dough.description }}</span>
                </label>
              </div>
            </div>
          </div>

          <div class="content__diameter">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите размер</h2>

              <div class="sheet__content diameter">
                <label
                  v-for="size in pizza.sizes"
                  :key="size.id"
                  class="diameter__input"
                  :class="{
                    'diameter__input--small': size.multiplier === 1,
                    'diameter__input--normal': size.multiplier === 2,
                    'diameter__input--big': size.multiplier === 3,
                  }"
                >
                  <input
                    type="radio"
                    name="diameter"
                    value="small"
                    class="visually-hidden"
                    checked
                  />
                  <span>{{ size.name }}</span>
                </label>
              </div>
            </div>
          </div>

          <div class="content__ingredients">
            <div class="sheet">
              <h2 class="title title--small sheet__title">
                Выберите ингредиенты
              </h2>

              <div class="sheet__content ingredients">
                <div class="ingredients__sauce">
                  <p>Основной соус:</p>

                  <label
                    v-for="sauce in pizza.sauces"
                    :key="sauce.id"
                    class="radio ingredients__input"
                  >
                    <input type="radio" name="sauce" value="tomato" checked />
                    <span>{{ sauce.name }}</span>
                  </label>
                </div>

                <div class="ingredients__filling">
                  <p>Начинка:</p>

                  <ul class="ingredients__list">
                    <li
                      v-for="ingredient in pizza.ingredients"
                      :key="ingredient.id"
                      class="ingredients__item"
                    >
                      <span
                        class="filling"
                        :class="{
                          'filling--mushrooms': ingredient.name === 'Грибы',
                          'filling--cheddar': ingredient.name === 'Чеддер',
                          'filling--salami': ingredient.name === 'Салями',
                          'filling--ham': ingredient.name === 'Ветчина',
                          'filling--ananas': ingredient.name === 'Ананас',
                          'filling--bacon': ingredient.name === 'Бекон',
                          'filling--onion': ingredient.name === 'Лук',
                          'filling--chile': ingredient.name === 'Чили',
                          'filling--jalapeno': ingredient.name === 'Халапеньо',
                          'filling--olives': ingredient.name === 'Маслины',
                          'filling--tomatoes': ingredient.name === 'Томаты',
                          'filling--salmon': ingredient.name === 'Лосось',
                          'filling--mozzarella':
                            ingredient.name === 'Моцарелла',
                          'filling--parmesan': ingredient.name === 'Пармезан',
                          'filling--blue_cheese': ingredient.name === 'Блю чиз',
                        }"
                      >
                        {{ ingredient.name }}
                      </span>

                      <div class="counter counter--orange ingredients__counter">
                        <button
                          type="button"
                          class="counter__button counter__button--minus"
                          disabled
                        >
                          <span class="visually-hidden">Меньше</span>
                        </button>
                        <input
                          type="text"
                          name="counter"
                          class="counter__input"
                          value="0"
                        />
                        <button
                          type="button"
                          class="counter__button counter__button--plus"
                        >
                          <span class="visually-hidden">Больше</span>
                        </button>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>

          <div class="content__pizza">
            <label class="input">
              <span class="visually-hidden">Название пиццы</span>
              <input
                type="text"
                name="pizza_name"
                placeholder="Введите название пиццы"
              />
            </label>

            <div class="content__constructor">
              <div class="pizza pizza--foundation--big-tomato">
                <div class="pizza__wrapper">
                  <div class="pizza__filling pizza__filling--ananas"></div>
                  <div class="pizza__filling pizza__filling--bacon"></div>
                  <div class="pizza__filling pizza__filling--cheddar"></div>
                </div>
              </div>
            </div>

            <div class="content__result">
              <p>Итого: 0 ₽</p>
              <button type="button" class="button" disabled>Готовьте!</button>
            </div>
          </div>
        </div>
      </form>
    </main>
  </body>
</template>

<script>
import misc from "@/static/misc.json";
import pizza from "@/static/pizza.json";
import user from "@/static/user.json";

export default {
  name: "views",
  data() {
    return {
      misc,
      pizza,
      user,
    };
  },
};
</script>

<style>
</style>
