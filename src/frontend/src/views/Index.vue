<template>
  <div class="">
    <header class="header">
      <div class="header__logo">
        <a href="index.html" class="logo">
          <img
            src="@/assets/img/logo.svg"
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
                  :class="`dough__input--${features.dough[dough.id]}`"
                >
                  <input
                    type="radio"
                    name="dought"
                    :value="features.dough[dough.id]"
                    class="visually-hidden"
                    :checked="dough.id == 1"
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
                  v-for="sizes in pizza.sizes"
                  :key="sizes.id"
                  class="diameter__input"
                  :class="`diameter__input--${features.diameter[sizes.id]}`"
                >
                  <input
                    type="radio"
                    name="diameter"
                    :value="features.diameter[sizes.id]"
                    class="visually-hidden"
                    :checked="sizes.id == 2"
                  />
                  <span>{{ sizes.name }}</span>
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
                    v-for="sauces in pizza.sauces"
                    :key="sauces.id"
                    class="radio ingredients__input"
                  >
                    <input
                      type="radio"
                      name="sauce"
                      :value="features.sauces[sauces.id]"
                      :checked="sauces.id == 1"
                    />
                    <span>{{ sauces.name }}</span>
                  </label>
                </div>

                <div class="ingredients__filling">
                  <p>Начинка:</p>

                  <ul class="ingredients__list">
                    <li
                      v-for="ingredients in pizza.ingredients"
                      :key="ingredients.id"
                      class="ingredients__item"
                    >
                      <span
                        class="filling"
                        :class="`filling--${features.ingr[ingredients.id]}`"
                      >
                        {{ ingredients.name }}
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
  </div>
</template>

<script>
import misc from "@/static/misc.json";
import pizza from "@/static/pizza.json";
import user from "@/static/user.json";

export default {
  name: "IndexHome",
  data() {
    return {
      misc,
      pizza,
      user,
      features: {
        dough: {
          1: "light",
          2: "large",
        },
        diameter: {
          1: "small",
          2: "normal",
          3: "big",
        },
        sauces: {
          1: "tomato",
          2: "creamy",
        },
        ingr: {
          1: "mushrooms",
          2: "cheddar",
          3: "salami",
          4: "ham",
          5: "ananas",
          6: "bacon",
          7: "onion",
          8: "chile",
          9: "jalapeno",
          10: "olives",
          11: "tomatoes",
          12: "salmon",
          13: "mozzarella",
          14: "parmesan",
          15: "blue_cheese",
        },
      },
    };
  },
};
</script>
<style style="scss" scoped></style>
