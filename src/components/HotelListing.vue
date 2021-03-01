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
      <div class="p-3 border rounded mb-3">
        <h2>Sorters</h2>
      </div>
      <cards-list class="padding-cards border rounded" :cards="cards" />
    </div>
  </div>
</template>
<script>
import CardsList from "./cards/CardsList";
const axios = require("axios").default;

export default {
  components: { CardsList },
  data() {
    return {
      cards: [],
    };
  },
  methods: {
    fetchCardsHandler() {
      axios
        .get("https://run.mocky.io/v3/90e1d920-afca-4101-8a97-9097310d7e8a")
        .then((response) => {
          // handle success
          console.log(response.data);
          this.cards = response.data;
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        })
        .then(function () {
          // always executed
        });
    },
  },
  mounted() {
    this.fetchCardsHandler();
  },
};
</script>

<style lang="scss" scoped>
.padding-cards {
  padding: 0.5em;
}
</style>