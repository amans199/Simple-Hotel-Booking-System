<template>
  <b-button @click="sortHandler" variant="primary" size="sm"
    >Sort by price
    <b-icon
      class="ml-1"
      :icon="sorted ? 'sort-numeric-down' : 'sort-numeric-up-alt'"
    ></b-icon
  ></b-button>
</template>
<script>
export default {
  data() {
    return {
      sorted: false,
    };
  },
  methods: {
    sortHandler() {
      this.sorted = !this.sorted;
    },
  },
};
</script>