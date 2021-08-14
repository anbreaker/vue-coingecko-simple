<template>
  <div class="container">
    <div class="row">
      <h1>Coin Market</h1>

      <input
        type="text"
        class="form-control text-light bg-dark rounded-0 border-0 my-4"
        placeholder="Search Coin"
        v-model="textSearch"
        @keyup="searchCoin()"
        autofocus
      />

      <table class="table table-hover table-dark text-light">
        <thead>
          <tr>
            <th v-for="(title, index) in titles" :key="index">
              {{ title }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(coin, index) in filteredCoins" :key="coin.id">
            <td class="text-muted">{{ index }}</td>
            <td>
              <img
                :src="coin.image"
                :alt="coin.name"
                style="width: 2rem"
                class="me-2"
              />
              <span>
                {{ coin.name }}
              </span>
              <span class="ms-2 text-muted text-uppercase">
                {{ coin.symbol }}
              </span>
            </td>
            <td>{{ coin.current_price.toLocaleString() }}</td>
            <td
              :class="[
                coin.price_change_percentage_24h > 0
                  ? 'text-success'
                  : 'text-danger',
              ]"
            >
              {{ coin.price_change_percentage_24h }}
            </td>
            <td>{{ coin.total_volume.toLocaleString() }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      coins: [],
      filteredCoins: [],
      titles: ["#", "Coin", "Price", "Price Change", "24h Volume"],
      textSearch: "",
    };
  },

  async mounted() {
    const response = await fetch(process.env.VUE_APP_API);

    const data = await response.json();
    this.coins = data;
    this.filteredCoins = data;
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