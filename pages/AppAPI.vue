<template>
    <AppHeader />
    <div class="container text-center mx-auto">
      <h1 class="my-4">CoinGecko</h1>
  
      <div class="mb-4">
        <input
          type="text"
          class="form-control text-dark bg-light rounded-0 border-0"
          placeholder="Search"
          v-model="textSearch"
          @keyup="searchCoin"
          autofocus
        />
       
      </div>
  
      <div class="mb-4">
        <label for="currency" class="text-dark mb-2">Select a currency:</label>
        <select id="currency" class="form-select text-dark bg-light rounded-0 border-0" v-model="selectedCurrency" @change="fetchCoins">
          <option value="usd">USD</option>
          <option value="eur">EUR</option>
          <option value="jpy">JPY</option>
          
        </select>
      </div>
  
      <table class="table table-hover table-light text-dark mx-auto">
        <thead>
          <tr>
            <th>#</th>
            <th>Coin</th>
            <th>Symbol</th>
            <th>Image</th>
            <th>Price</th>
            <th>Price Change</th>
            <th>24h Volume</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(coin, index) in filteredCoins" :key="coin.id">
            <td class="text-muted">{{ index + 1 }}</td>
            <td>
              <span>
                {{ coin.name }}
              </span>
            </td>
            <td>{{ coin.symbol }}</td>
            <td>
              <img :src="coin.image" :alt="coin.name" style="width: 2rem" />
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
  </template>
  
  <script>
  export default {
    name: "App",
    data() {
      return {
        coins: [],
        filteredCoins: [],
        titles: ["#", "Coin", "Symbol", "Image", "Price", "Price Change", "24h Volume"],
        textSearch: "",
        selectedCurrency: "usd",
      };
    },
    async mounted() {
      await this.fetchCoins();
    },
    methods: {
      async fetchCoins() {
        try {
          const response = await fetch(
            `https://api.coingecko.com/api/v3/coins/markets?vs_currency=${this.selectedCurrency}&order=market_cap_desc&per_page=10&page=1&sparkline=false&x_cg_demo_api_key=CG-BqhoEtTCKLszVNmzyE2iLng2`
          );
  
          const data = await response.json();
          this.coins = data;
          this.filteredCoins = data;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      },
      searchCoin() {
        this.filteredCoins = this.coins.filter(
          (coin) =>
            coin.name.toLowerCase().includes(this.textSearch.toLowerCase()) ||
            coin.symbol.toLowerCase().includes(this.textSearch.toLowerCase())
        );
      },
      performSearch() {
        
      },
    },
  };
  </script>
  
  <style>
  .container {
    margin: 20px auto;
    text-align: center;
  }
  
  .table {
    width: 100%;
  }
  
  .table th, .table td {
    border: 1px solid #e4dede;
    padding: 10px;
    text-align: center;
  }
  
  .text-muted {
    color: #444;
  }
  
  .text-success {
    color: #28a745;
  }
  
  .text-danger {
    color: #dc3545;
  }
  
  .mb-4 {
    margin-left: 100;
    display: relative; 
    padding: 1px;
    margin: 10px;
  }
  </style>
  