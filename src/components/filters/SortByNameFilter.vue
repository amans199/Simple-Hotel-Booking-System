<template>
  <b-button @click="sortHandler" variant="primary" size="sm"
    >Sort by name
    <b-icon
      class="ml-1"
      :icon="sorted ? 'sort-alpha-down' : 'sort-alpha-up-alt'"
    ></b-icon
  ></b-button>
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
      sorted: false,
      cardsSorted: [],
    };
  },
  methods: {
    sortHandler() {
      this.sorted = !this.sorted;
      let order = this.sorted ? -1 : 1;
      this.cardsSorted = this.cards.sort(
        (a, b) =>
          order *
          a.name.localeCompare(b.name, "en", { ignorePunctuation: true })
      );
      this.$emit("cardSortedByName", this.cardsSorted);
    },
  },
};
</script>