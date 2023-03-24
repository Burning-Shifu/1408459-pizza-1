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
                <BuilderDoughSelector
                  v-for="dough in pizza.dough"
                  :key="dough.id"
                  class="dough__input"
                  :class="`dough__input--${features.dough[dough.id]}`"
                  :dough="dough"
                  :featuresDough="features.dough"
                  @doughValue="getDoughValue"
                />
              </div>
            </div>
          </div>

          <div class="content__diameter">
            <div class="sheet">
              <h2 class="title title--small sheet__title">Выберите размер</h2>

              <div class="sheet__content diameter">
                <BuilderSizeSelector
                  v-for="sizes in pizza.sizes"
                  :key="sizes.id"
                  class="diameter__input"
                  :class="`diameter__input--${features.sizes[sizes.id]}`"
                  :sizes="sizes"
                  :featuresSizes="features.sizes"
                  @sizeValue="getSizeValue"
                />
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

                  <BuilderSausesSelector
                    v-for="sauces in pizza.sauces"
                    :key="sauces.id"
                    class="radio ingredients__input"
                    :sauces="sauces"
                    :featuresSauces="features.sauces"
                    @saucesValue="getSaucesValue"
                  />
                </div>

                <div class="ingredients__filling">
                  <p>Начинка:</p>

                  <ul class="ingredients__list">
                    <BuilderIngredientsSelector
                      v-for="ingredients in pizza.ingredients"
                      :key="ingredients.id"
                      class="ingredients__item"
                      :ingredients="ingredients"
                      :featuresIngr="features.ingr"
                      @ingredientValue="getIngredientsValue"
                    />
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
              <BuilderPizzaView
                class="pizza"
                :class="`pizza--foundation--${order.doughValue}-${order.saucesValue}`"
                :orderIngredients="order.ingredientsValue"
              />
            </div>

            <BuilderPriceCounter
              :order="order"
              :pizza="pizza"
              :features="features"
              @priceValue="getPriceValue"
            />
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
import BuilderDoughSelector from "@/modules/builder/components/BuilderDoughSelector";
import BuilderPizzaView from "@/modules/builder/components/BuilderPizzaView";
import BuilderSausesSelector from "@/modules/builder/components/BuilderSausesSelector";
import BuilderIngredientsSelector from "@/modules/builder/components/BuilderIngredientsSelector";
import BuilderSizeSelector from "@/modules/builder/components/BuilderSizeSelector";
import BuilderPriceCounter from "@/modules/builder/components/BuilderPriceCounter";

export default {
  name: "IndexHome",
  components: {
    BuilderDoughSelector,
    BuilderPizzaView,
    BuilderSausesSelector,
    BuilderIngredientsSelector,
    BuilderSizeSelector,
    BuilderPriceCounter,
  },
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
        sizes: {
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
      order: {
        doughValue: "light",
        sizeValue: "normal",
        saucesValue: "tomato",
        ingredientsValue: {},
      },
      price: 0,
      // target: "",
    };
  },
  methods: {
    getDoughValue(value) {
      this.order.doughValue = value;
      console.log("child component said: DoughValue", value);
    },
    getSaucesValue(value) {
      this.order.saucesValue = value;
      console.log("child component said: SaucesValue", value);
    },
    getSizeValue(value) {
      this.order.sizeValue = value;
      this.$forceUpdate();
      console.log("child component said: SizeValue", value);
    },
    getIngredientsValue(value, target) {
      if (target.classList.contains("counter__button--plus")) {
        if (value in this.order.ingredientsValue === false) {
          this.$set(this.order.ingredientsValue, value, 1);
        } else if (this.order.ingredientsValue[value] < 3) {
          let num = this.order.ingredientsValue[value];
          this.order.ingredientsValue[value] = num + 1;
        } else {
          alert("Кол-во одинаковых ингредиентов не может быть больше 3");
        }
      } else {
        if (this.order.ingredientsValue[value] > 1) {
          let num = this.order.ingredientsValue[value];
          this.order.ingredientsValue[value] = num - 1;
        } else if (this.order.ingredientsValue[value] == 1) {
          this.$delete(this.order.ingredientsValue, value);
        }
      }

      this.$forceUpdate();
      console.log("child component said: IngredientValue", value);
      console.log("order IngredientsValue", this.order.ingredientsValue);
    },
    getPriceValue(value) {
      this.price = value;
      console.log("child component said: PriceValue", value);
    },
  },
  watch: {
    order: {
      handler: function () {
        this.getPriceValue();
      },
      deep: true,
    },
  },
};
</script>
<style style="scss" scoped></style>
