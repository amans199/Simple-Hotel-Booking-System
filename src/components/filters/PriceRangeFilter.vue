<template>
  <b-form-group label="Price Range">
    <b-form-input
      id="range-1"
      v-model="value"
      type="range"
      :min="minVal"
      :max="maxVal"
      @change="FilterCardsByPriceRangeHandler"
      variant="secondary"
    ></b-form-input>
    <div class="d-flex align-items-center justify-content-between w-100">
      <span>{{ minVal }}</span>
      <b-button variant="secondary" disabled>{{ value }}</b-button>
      <span>{{ maxVal }}</span>
    </div>
  </b-form-group>
</template>
<script>
export default {
  props: {
    cards: {
      type: Array,
    },
  },
  data() {
    return {
      value: 0,
      minVal: 0,
      maxVal: 0,
      initialCards: [...this.cards],
      cardFiltered: [],
    };
  },
  methods: {
    setMinValueHandler() {
      this.minVal = [...this.cards].reduce(
        (a, b) => (a.price < b.price ? a : b),
        0
      ).price;
    },
    setMaxValueHandler() {
      this.maxVal = [...this.cards].reduce(
        (a, b) => (a.price > b.price ? a : b),
        0
      ).price;
    },
    FilterCardsByPriceRangeHandler() {
      this.cardFiltered = this.initialCards.filter(
        (a) => a.price <= this.value
      );
      this.$emit("cardsInPriceRangeFiltered", this.cardFiltered);
    },
  },
  mounted() {
    this.setMinValueHandler();
    this.setMaxValueHandler();
  },
};
</script>