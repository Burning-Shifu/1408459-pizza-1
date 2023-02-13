<template>
  <label>
    <input
      type="radio"
      name="dough"
      :value="featuresDough[dough.id]"
      @click="sendDoughValue"
      class="visually-hidden"
      :checked="dough.id == 1"
    />
    <!-- :checked="dough.id == 1" -->
    <!-- :checked="features.dough[dough.id] == doughValue" -->
    <b>{{ dough.name }}</b>
    <span>{{ dough.description }}</span>
  </label>
</template>

<script>
export default {
  name: "BuilderDoughSelector",
  data() {
    return {
      doughValue: this.featuresDough[this.dough.id],
    };
  },
  props: {
    dough: {
      type: Object,
      required: true,
    },
    featuresDough: {
      type: Object,
      required: true,
    },
  },
  methods: {
    sendDoughValue() {
      this.$emit("doughValue", this.doughValue);
      console.log(this.doughValue);
    },
  },
};
</script>
