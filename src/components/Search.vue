<template>
  <input
    type="text"
    class="form-control text-light bg-dark rounded-0 border-0 my-4"
    placeholder="Search Coin"
    v-model="textSearch"
    @keyup="searchCoin()"
    autofocus
  />
</template>

<script>
export default {
  name: "Search",

  props: ["coins"],

  data() {
    return {
      filteredCoins: [],
      textSearch: "",
    };
  },

  methods: {
    searchCoin() {
      this.filteredCoins = this.coins.filter(
        (coin) =>
          coin.name.toLowerCase().includes(this.textSearch.toLowerCase()) ||
          coin.symbol.toLowerCase().includes(this.textSearch.toLowerCase())
      );
    },
  },
};
</script>

