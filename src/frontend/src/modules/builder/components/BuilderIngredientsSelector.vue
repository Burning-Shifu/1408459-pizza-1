<template>
  <li>
    <span class="filling" :class="`filling--${featuresIngr[ingredients.id]}`">
      {{ ingredients.name }}
    </span>

    <div class="counter counter--orange ingredients__counter">
      <button
        type="button"
        class="counter__button counter__button--minus"
        @click="sendIngredientValue($event.target), minusCounterIngredient()"
        :disabled="ingredientCounter == 0"
      >
        <span class="visually-hidden">Меньше</span>
      </button>
      <input
        type="text"
        name="counter"
        class="counter__input"
        value="0"
        v-model="ingredientCounter"
      />
      <button
        type="button"
        class="counter__button counter__button--plus"
        :value="featuresIngr[ingredients.id]"
        @click="sendIngredientValue($event.target), plusCounterIngredient()"
        :disabled="ingredientCounter >= 3"
      >
        <span class="visually-hidden">Больше</span>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "BuilderIngredientsSelector.vue",
  data() {
    return {
      ingredientCounter: 0,
      ingredientValue: this.featuresIngr[this.ingredients.id],
    };
  },
  props: {
    ingredients: {
      type: Object,
      required: true,
    },
    featuresIngr: {
      type: Object,
      required: true,
    },
  },
  methods: {
    sendIngredientValue(target) {
      this.$emit("ingredientValue", this.ingredientValue, target);
      console.log(this.ingredientValue);
    },
    plusCounterIngredient() {
      if (this.ingredientCounter < 3) this.ingredientCounter += 1;
    },
    minusCounterIngredient() {
      if (this.ingredientCounter > 0) this.ingredientCounter -= 1;
    },
  },
};
</script>
