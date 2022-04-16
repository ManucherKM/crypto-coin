<template>
  <div class="parent">
    <div class="parent__block-stats">
      <h1 class="text-center">Общая статистика</h1>
      <p class="parent__total-coin">
        Всего различных монет на рынке: <strong>{{ mas.data.stats.total }}</strong>
      </p>
      <p class="parent__total-coin">
        Всего монет на рынке: <strong>{{ mas.data.stats.totalCoins }}</strong>
      </p>
      <p class="parent__total-coin">
        Количество рынков: <strong>{{ mas.data.stats.totalMarkets }}</strong>
      </p>
      <p class="parent__total-coin">
        Общая рыночная капитализация: <strong>{{ mas.data.stats.totalMarketCap }}</strong>
      </p>
      <p class="parent__total-coin">
        Объем за последние 24 часа: <strong>{{ mas.data.stats.total24hVolume }}</strong>
      </p>
      <h1 class="text-center">Три лучшие монеты</h1>
      <p class="parent__total-coin">
        1 место: <strong>{{ mas.data.stats.bestCoins[0].name }}</strong>
      </p>
      <p class="parent__total-coin">
        2 место: <strong>{{ mas.data.stats.bestCoins[1].name }}</strong>
      </p>
      <p class="parent__total-coin">
        3 место: <strong>{{ mas.data.stats.bestCoins[2].name }}</strong>
      </p>
      <h1 class="text-center">Самые популярные монеты</h1>
      <p class="parent__total-coin">
        1 место: <strong>{{ mas.data.stats.newestCoins[0].name }}</strong>
      </p>
      <p class="parent__total-coin">
        2 место: <strong>{{ mas.data.stats.newestCoins[1].name }}</strong>
      </p>
      <p class="parent__total-coin">
        3 место: <strong>{{ mas.data.stats.newestCoins[2].name }}</strong>
      </p>
    </div>
    <h1 class="text-center">Новейшие монеты</h1>
    <div class="coin">
      <div v-for="coin in mas.data.coins" :key="coin.symbol" class="clone">
        <CardApi :srcImg="coin.iconUrl" :altSrc="coin.symbol" :coinName="coin.name" :coinPrice="coin.price" />
      </div>
      <!-- {{ mas.data.stats }} -->
    </div>
  </div>


</template>

<script>

import axios from "axios";
import CardApi from "../components/cardApi.vue";

export default {
  name: "IndexPage",
  data() {
    return {
      mas: [],
    };
  },
  async asyncData() {
    const options = {
      method: "GET",
      url: "https://coinranking1.p.rapidapi.com/coins",
      params: {
        referenceCurrencyUuid: "yhjMzLPhuIDl",
        timePeriod: "24h",
        tiers: "1",
        orderBy: "marketCap",
        orderDirection: "desc",
        limit: "50",
        offset: "0"
      },
      headers: {
        "X-RapidAPI-Host": "coinranking1.p.rapidapi.com",
        "X-RapidAPI-Key": "76d7e06148msh263d850659d08bdp1c483cjsnf26e619a4a8c"
      }
    };
    try {
      const response = await axios.request(options);
      return {
        mas: response.data
      };
    }
    catch (error) {
      console.error(error);
    }
  },
  components: { CardApi }
}
</script>

<style>
.clone {
  width: min-content;
  height: min-content;
}

.coin {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 350px;
  grid-column-gap: 5px;
}

.parent {
  padding-top: 10px;
  width: 90%;
  margin: 0 auto;
}

.parent h1 {
  margin: 40px;
}
</style>
