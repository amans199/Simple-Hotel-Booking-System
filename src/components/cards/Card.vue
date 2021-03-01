<template>
  <b-card tag="article" class="gap-1em w-50-with-gap text-left">
    <p>Name: {{ card.name }}</p>
    <p>Price: {{ card.price }}</p>
    <address>City: {{ card.city }}</address>
    <p>
      Available on:
      <time :date="card.available_on">{{ card.available_on }}</time>
    </p>
  </b-card>
</template>
<script>
export default {
  props: {
    card: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.gap-1em {
  margin: 0.5em;
}
.w-50-with-gap {
  width: calc(50% - 1em);
}
</style>