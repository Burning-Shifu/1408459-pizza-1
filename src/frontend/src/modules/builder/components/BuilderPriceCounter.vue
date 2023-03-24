<template>
  <div class="content__result">
    <p>Итого: {{ priceValue }} ₽</p>
    <button type="button" class="button">Готовьте!</button>
  </div>
</template>

<script>
export default {
  name: "BuilderPriceCounter.vue",
  data() {
    return {
      priceValue: 0,
      doughPrice: 0,
      saucePrice: 0,
      sizeMultiplier: 0,
      ingredientsPrice: 0,
    };
  },
  props: {
    features: {
      type: Object,
      required: true,
    },
    order: {
      type: Object,
      required: true,
    },
    pizza: {
      type: Object,
      required: true,
    },
  },
  watch: {
    order: {
      handler: function () {
        this.countPrice();
        this.sendPriceValue();
      },
      deep: true,
    },
  },
  methods: {
    countPrice() {
      // find ordered size multiplier
      for (const prop in this.features.sizes) {
        if (this.features.sizes[prop] === this.order.sizeValue) {
          let key = prop;
          const pizzaSizeObj = this.pizza.sizes.find((u) => u.id === +key);
          this.sizeMultiplier = pizzaSizeObj.multiplier;
          break;
        }
      }

      // find ordered dough price
      for (const prop in this.features.dough) {
        if (this.features.dough[prop] === this.order.doughValue) {
          let key = prop;
          const pizzaDoughObj = this.pizza.dough.find((u) => u.id === +key);
          this.doughPrice = pizzaDoughObj.price;
          break;
        }
      }

      // find ordered sauce price
      for (const prop in this.features.sauces) {
        if (this.features.sauces[prop] === this.order.saucesValue) {
          let key = prop;
          const pizzaSaucesObj = this.pizza.sauces.find((u) => u.id === +key);
          this.saucePrice = pizzaSaucesObj.price;
          break;
        }
      }

      // find price of all ordered ingredients
      let ingrPricesArr = [];

      for (const prop in this.features.ingr) {
        //check if object of ingr is NOT empty
        if (Object.keys(this.order.ingredientsValue).length !== 0) {
          for (const orderProp in this.order.ingredientsValue) {
            if (this.features.ingr[prop] === orderProp) {
              let key = prop;
              const pizzaIngredientsObj = this.pizza.ingredients.find(
                (u) => u.id === +key
              );

              //add a price of every ingr in the array
              ingrPricesArr.push(
                pizzaIngredientsObj.price *
                  this.order.ingredientsValue[orderProp]
              );

              // sum all prices in the array and assign to a price property
              this.ingredientsPrice = ingrPricesArr.reduce((a, b) => a + b, 0);

              break;
            }
          }
        } else {
          this.ingredientsPrice = 0;
        }
      }

      this.priceValue =
        this.sizeMultiplier *
        (this.doughPrice + this.saucePrice + this.ingredientsPrice);
    },
    sendPriceValue() {
      this.$emit("priceValue", this.priceValue);
      console.log(this.priceValue);
    },
  },
};
</script>
