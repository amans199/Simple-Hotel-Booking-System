<template>
  <div class="d-flex flex-wrap">
    <card v-for="(card, index) in cards" :key="index" />
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
  },
  components: { Card },
};
</script>