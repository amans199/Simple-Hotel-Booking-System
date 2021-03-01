<template>
  <div>
    <b-spinner v-if="loadingCards" />
    <b-alert show v-if="cards.length == 0 && !loadingCards" class="mb-0"
      >No Available Hotels, please try another search</b-alert
    >
    <div class="d-flex flex-wrap">
      <card v-for="(card, index) in cards" :key="index" :card="card" />
    </div>
  </div>
</template>
<script>
import Card from "./Card";
export default {
  props: {
    cards: {
      type: Array,
      required: true,
    },
    loadingCards: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  components: { Card },
};
</script>