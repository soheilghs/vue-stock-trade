<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-info">

      <div class="panel-heading">
        <h3 class="panel-title">
          {{ stock.name }}
          <small>
            (Price: {{ stock.price }} |
            Quantity: {{ stock.quantity }})
          </small>
        </h3>
      </div>

      <div class="panel-body">
        <div class="row">
          <div class="pull-left col-lg-6">
            <input type="number" class="form-control"
                   :class="{danger: insufficientQuantity}"
                   placeholder="Quantity" v-model="quantity">
          </div>
          <div class="pull-right mr-10">
            <button class="btn btn-success" @click="sellStock"
                    :disabled="insufficientQuantity || quantity <= 0
                   || !Number.isInteger(+quantity)">
              {{ insufficientQuantity ? 'Not enough Stocks' : 'Sell' }}
            </button>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import {mapActions} from 'vuex';

export default {
  name: "StockPage",
  props: ['stock'],
  data() {
    return {
      quantity: 0
    }
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock'
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }

      console.log(order);

      this.placeSellOrder(order);
      this.quantity = 0;
    }
  }
}
</script>

<style scoped>
.mr-10 {
  margin-right: 10px;
}

.danger {
  border: 1px solid red;
}
</style>