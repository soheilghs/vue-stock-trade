<template>
  <div>
    <app-stock v-for="(stock, i) in stocks" v-bind:key="i"
               :stock="stock">
    </app-stock>
  </div>
</template>

<script>
import Stock from "@/components/stocks/Stock";

export default {
  name: "StocksPage",
  components: {
    appStock: Stock
  },
  computed: {
    stocks() {
      return this.$store.getters.stocks;
    }
  }
}
</script>