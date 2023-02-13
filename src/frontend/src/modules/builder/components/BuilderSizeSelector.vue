<template>
  <label>
    <input
      type="radio"
      name="diameter"
      :value="features.sizes[sizes.id]"
      class="visually-hidden"
      :checked="sizes.id == 2"
    />
    <span>{{ sizes.name }}</span>
  </label>
</template>

<script>
export default {
  name: "BuilderSizeSelector.vue",
  data() {
    return {
      saucesValue: this.featuresSizes[this.sizes.id],
    };
  },
  props: {
    sizes: {
      type: Object,
      required: true,
    },
    featuresSizes: {
      type: Object,
      required: true,
    },
  },
  methods: {
    sendSizesValue() {
      this.$emit("sizesValue", this.sizesValue);
      console.log(this.sizesValue);
    },
  },
};
</script>
