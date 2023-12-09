<template>
  <div>
    <app-stock v-for="(stock, i) in stocks" v-bind:key="i"
               :stock="stock"></app-stock>
  </div>
</template>

<script>
import {mapGetters} from 'vuex';
import Stock from './Stock';

export default {
  name: "PortfolioPage",
  computed: {
    ...mapGetters({
      stocks: 'stockPortfolio'
    })
  },
  components: {
    appStock: Stock
  }
}
</script>