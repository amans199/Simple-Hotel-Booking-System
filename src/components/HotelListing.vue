<template>
  <div class="row">
    <aside class="col-md-3 pr-md-0">
      <div class="p-3 border rounded">
        <search-filter
          :cards="cardsFiltered"
          @cardsSearched="cardsSearchedHandler"
        />
      </div>
    </aside>
    <div class="col-md-9">
      <div
        class="p-3 border rounded mb-3 d-flex flex-column flex-md-row align-items-md-center justify-content-center justify-content-md-between"
      >
        <p class="mb-0 font-weight-bold">
          Total Hotels : {{ cardsFiltered.length }}
        </p>
        <section>
          <sort-by-name :cards="cardsFiltered" class="mr-1" />
          <sort-by-price :cards="cardsFiltered" class="ml-1" />
        </section>
      </div>
      <cards-list
        class="padding-cards border rounded"
        :cards="cardsFiltered"
        :loadingCards="loadingCards"
        :class="loadingCards ? 'cards-container ' : ''"
      />
    </div>
  </div>
</template>
<script>
import CardsList from "./cards/CardsList";
import SortByName from "./filters/SortByNameFilter";
import SortByPrice from "./filters/SortByPriceFilter";
import SearchFilter from "./filters/SearchFilter";
const axios = require("axios").default;
import { EventBus } from "../event-bus";

export default {
  components: { CardsList, SortByName, SortByPrice, SearchFilter },
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
        .catch((error) => {
          console.log(error);
          this.loadingCards = false;
        });
    },
    // todo : resole the same approach as the other filters
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
    cardsSearchedHandler(searchVal, searchedCards) {
      searchVal == ""
        ? (this.cardsFiltered = this.cards)
        : (this.cardsFiltered = searchedCards);
    },
  },
  mounted() {
    // Filter : Date Range
    this.fetchCardsHandler();
    EventBus.$on("FilterDateRange", (start, end) => {
      this.filterCardsbyDateRange(start, end);
    });

    // Reset Date Range Filter
    EventBus.$on("ResetFilterDateRange", (value) => {
      this.cardsFiltered = this.cards;
    });

    // Sort By Name
    this.$on("cardSortedByName", (cardsSortedArr) => {
      this.cardsFiltered = cardsSortedArr;
    });

    // Sort By Price
    this.$on("cardSortedByPrice", (cardsSortedArr) => {
      this.cardsFiltered = cardsSortedArr;
    });
  },
};
</script>

<style lang="scss" scoped>
.padding-cards {
  padding: 0.5em;
}
.cards-container {
  min-height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>