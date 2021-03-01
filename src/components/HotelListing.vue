<template>
  <div class="row">
    <aside class="col-md-3 pr-md-0">
      <div class="p-3 border rounded">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Minus assumenda
        exercitationem ut labore alias excepturi sed reiciendis ipsam corporis,
        possimus nobis molestiae, blanditiis iusto, voluptatibus culpa
        temporibus cupiditate! Rerum, voluptatibus?s
      </div>
    </aside>
    <div class="col-md-9">
      <!-- <list-header></list-header> -->
      <div
        class="p-3 border rounded mb-3 d-flex flex-column flex-md-row align-items-md-center justify-content-center justify-content-md-between"
      >
        <h2 class="mb-0">Sorters</h2>
        <section>
          <sort-by-name class="mr-1" />
          <sort-by-price class="ml-1" />
        </section>
      </div>
      <cards-list
        class="padding-cards border rounded"
        :cards="cardsFiltered"
        :loadingCards="loadingCards"
      />
    </div>
  </div>
</template>
<script>
import CardsList from "./cards/CardsList";
import SortByName from "./filters/SortByNameFilter";
import SortByPrice from "./filters/SortByPriceFilter";
const axios = require("axios").default;
import { EventBus } from "../event-bus";

export default {
  components: { CardsList, SortByName, SortByPrice },
  data() {
    return {
      cards: [],
      cardsFiltered: [],
      loadingCards: false,
    };
  },
  methods: {
    fetchCardsHandler() {
      this.loadingCards = true;
      axios
        .get("https://run.mocky.io/v3/90e1d920-afca-4101-8a97-9097310d7e8a")
        .then((response) => {
          this.cards = response.data;
          this.cardsFiltered = response.data;
          this.loadingCards = false;
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    filterCardsbyDateRange(fromVal, toVal) {
      this.loadingCards = true;
      this.cardsFiltered = this.cards.filter((card) => {
        let CardDate = new Date(card.available_on).getTime();
        return fromVal <= CardDate && CardDate <= toVal;
      });
      setTimeout(() => {
        this.loadingCards = false;
      }, 500);
    },
  },
  mounted() {
    this.fetchCardsHandler();
    EventBus.$on("FilterDateRange", (start, end) => {
      this.filterCardsbyDateRange(start, end);
    });
    EventBus.$on("ResetFilterDateRange", (value) => {
      this.cardsFiltered = this.cards;
    });
  },
};
</script>

<style lang="scss" scoped>
.padding-cards {
  padding: 0.5em;
}
</style>