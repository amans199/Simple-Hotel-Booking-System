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