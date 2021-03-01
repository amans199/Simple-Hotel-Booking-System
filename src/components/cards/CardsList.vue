<template>
  <div>
    <b-spinner v-if="loadingCards" />
    <b-alert show v-if="cards.length == 0 && !loadingCards" class="mb-0"
      >No Available Hotels, please try another search</b-alert
    >
    <transition-group
      name="filter_cards_transition"
      tag="div"
      class="d-flex flex-wrap"
      v-if="!loadingCards"
    >
      <card
        v-for="card in cards"
        :key="card.name.replace(' ', '_')"
        :card="card"
      />
    </transition-group>
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

<style lang="scss">
.filter_cards_transition {
  position: relative;
  width: calc(100% / 2 - 1rem);
  display: inline-flex;
  flex-direction: column;
  justify-content: space-between;
  margin-left: 1rem;
  margin-top: 1rem;
  padding-top: 0.75rem;
  border-radius: 6px;
  background-color: white;
  box-shadow: 0 0 0 1px #c5d0d1;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  transform-origin: 10% 50%;
  z-index: 1;
  @media (min-width: 800px) {
    width: calc(100% / 3 - 1rem);
  }

  &-move {
    transition: all 600ms ease-in-out 50ms;
  }
  &-enter-active {
    transition: all 300ms ease-out;
  }

  &-leave-active {
    transition: all 200ms ease-in;
    position: absolute;
    z-index: 0;
  }

  &-enter,
  &-leave-to {
    opacity: 0;
  }
  &-enter {
    transform: scale(0.9);
  }
}
</style>