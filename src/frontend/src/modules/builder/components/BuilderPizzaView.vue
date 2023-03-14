<template>
  <div>
    <div class="pizza__wrapper"></div>
  </div>
</template>

<script>
export default {
  name: "BuilderPizzaView.vue",
  data() {
    return {};
  },
  props: {
    orderIngredients: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addIngredient() {
      this.$root.$on("add-to-pizza-view", (value) => {
        let pizzaView = document.querySelector(".pizza__wrapper"),
          ingr = document.createElement("div");

        switch (this.orderIngredients[value]) {
          case 1:
            ingr.classList.add("pizza__filling", `pizza__filling--${value}`);
            break;
          case 2:
            ingr.classList.add(
              "pizza__filling",
              `pizza__filling--${value}`,
              "pizza__filling--second"
            );
            break;
          case 3:
            ingr.classList.add(
              "pizza__filling",
              `pizza__filling--${value}`,
              "pizza__filling--third"
            );
            break;
          default:
            break;
        }

        pizzaView.append(ingr);
      });
    },

    deleteIngredient() {
      this.$root.$on("delete-from-pizza-view", (value) => {
        let pizzaView = document.querySelector(".pizza__wrapper"),
          ingrArray = pizzaView.querySelectorAll(`.pizza__filling--${value}`);

        switch (ingrArray.length) {
          case 1:
            pizzaView.querySelector(`.pizza__filling--${value}`).remove();
            break;
          case 2:
            pizzaView
              .querySelector(`.pizza__filling--${value}.pizza__filling--second`)
              .remove();
            break;
          case 3:
            pizzaView
              .querySelector(`.pizza__filling--${value}.pizza__filling--third`)
              .remove();
            break;
          default:
            break;
        }
      });
    },
    setupIngredients() {
      this.addIngredient();
      this.deleteIngredient();
    },
  },
  mounted() {
    this.setupIngredients();
  },
};
</script>
