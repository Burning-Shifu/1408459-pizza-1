<template>
  <label>
    <input
      type="radio"
      name="sauce"
      :value="featuresSauces[sauces.id]"
      @click="sendSaucesValue"
      :checked="sauces.id == 1"
    />
    <span>{{ sauces.name }}</span>
  </label>
</template>

<script>
export default {
  name: "BuilderSausesSelector.vue",
  data() {
    return {
      saucesValue: this.featuresSauces[this.sauces.id],
    };
  },
  props: {
    sauces: {
      type: Object,
      required: true,
    },
    featuresSauces: {
      type: Object,
      required: true,
    },
  },
  methods: {
    sendSaucesValue() {
      this.$emit("saucesValue", this.saucesValue);
      console.log(this.saucesValue);
    },
  },
};
</script>
