<template>
  <div>

    <a @click="show='customers'">SHOW_CUSTOMERS</a><br>
    <a @click="show='orders'">SHOW_ORDERS</a>
    <Customers v-show="show=='customers'"/>
    <Orders v-show="show=='orders'"/>
  </div>
</template>

<script>
import * as _ from 'lodash';
import Customers from './Customers.vue';
import Orders from './Orders.vue';

export default {

  name: 'Demo',
  data: function () {
    return {
      num: 12,
      show: ''
    };
  },

  components: {
    Customers,
    Orders,
  },

  computed: {
    mul: function() {
      return this.num+this.num2;
    },
    arr: function () {
      return _.range(2, this.num, 2);
    }
  },
  props: {
    num2: {
      type: Number,
    }
  },
}

</script>
