<template>
  <label>
    <input
      type="radio"
      name="diameter"
      :value="featuresSizes[sizes.id]"
      @click="sendSizeValue"
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
      sizeValue: this.featuresSizes[this.sizes.id],
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
    sendSizeValue() {
      this.$emit("sizeValue", this.sizeValue);
      // console.log(this.sizeValue);
    },
  },
};
</script>
