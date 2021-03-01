<template>
  <div
    class="row mx-0 d-flex flex-column flex-md-row align-items-center justify-content-center border rounded p-3"
  >
    <aside class="col-md-4"></aside>
    <div class="col-md-8">
      <!-- <list-header></list-header> -->
      <h2>Sorters</h2>
      <cards-list />
    </div>
  </div>
</template>
<script>
import CardsList from "./cards/CardsList";

export default {
  components: { CardsList },
  methods: {
    //
  },
};
</script>