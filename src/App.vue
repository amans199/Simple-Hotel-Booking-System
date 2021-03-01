<template>
  <main id="app" class="my-5 container">
    <date-range-filter class="my-3" />
    <!-- <transition name="slide"> </transition> -->
    <hotel-listing class="my-3" />
  </main>
</template>

<script>
import DateRangeFilter from "./components/filters/DateRangeFilter";
import HotelListing from "./components/HotelListing";

export default {
  name: "App",
  components: { DateRangeFilter, HotelListing },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
