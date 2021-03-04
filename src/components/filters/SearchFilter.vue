<template>
  <div>
    <b-form-group label="Search">
      <b-form-input
        v-model="searchVal"
        placeholder="Search"
        @input="searchHandler"
        type="search"
      ></b-form-input>
    </b-form-group>
  </div>
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
      searchVal: "",
      searchedCards: [],
      waitForUserToFinishWriting: false,
    };
  },
  methods: {
    searchHandler() {
      this.searchedCards = this.cards;
      if (this.searchVal) {
        this.searchedCards = this.cards.filter(
          (ele) =>
            ele.name.toLowerCase().indexOf(this.searchVal.toLowerCase()) !== -1
        );
      }
      this.$emit("cardsSearched", this.searchVal, this.searchedCards);
    },
  },
  mounted() {},
  watch: {
    // searchVal: function (val) {
    //   if (!this.waitForUserToFinishWriting) {
    //     setTimeout(() => {
    //       this.waitForUserToFinishWriting = false;
    //       this.$emit("cardsSearched", this.searchedCards);
    //     }, 300);
    //     this.waitForUserToFinishWriting = true;
    //   }
    // },
  },
};
</script>