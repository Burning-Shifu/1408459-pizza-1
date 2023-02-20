<template>
  <li>
    <span class="filling" :class="`filling--${featuresIngr[ingredients.id]}`">
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
      <input type="text" name="counter" class="counter__input" value="0" />
      <button
        type="button"
        class="counter__button counter__button--plus"
        :value="featuresIngr[ingredients.id]"
        @click="sendIngredientValue"
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
    sendIngredientValue() {
      this.$emit("ingredientValue", this.ingredientValue);
      console.log(this.ingredientValue);
    },
  },
};
</script>
