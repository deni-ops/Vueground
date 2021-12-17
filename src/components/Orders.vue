<template lang="html">
  <div>
    <h2>Orders</h2>

    <el-button plain @click="getData">Update</el-button>
    <el-button plain @click="orders=[]">Reset</el-button>

    <el-table :data="orders">

      <el-table-column prop="customer_id" label="CustomerID">
        <template #default="scope">
          <a @click="showDetails(scope.row.customer_id)">
            {{scope.row.customer_id}}
            <!-- {{customerData}} -->
          </a>
        </template>
      </el-table-column>

      <el-table-column prop="ship_name" label="ShipName" sortable/>
      <el-table-column prop="ship_address" label="ShipAddress"/>
    </el-table>

    <el-dialog v-model="showDialog" title="CustomerDetails">

      <!-- {{customerId}} -->

      <el-table :data="customerTable">
        <el-table-column prop="name" label="Name"/>
        <el-table-column prop="value" label="Value"/>
        <!-- {{customerTable}} -->
      </el-table>
      <el-button @click="showDialog = false">Close</el-button>
    </el-dialog>

  </div>
</template>

<script>
import axios from 'axios';

export default
{
  name: 'Demo',
  data:
    function()
    {
      return {
        orders: [],
        loading: false,
        showDialog: false,
        customerId: null,
        customerData: null,
      };
    },
  methods:
  {
      getData: function() {
          var self = this;
          this.orders = [];
          this.loading = true;
          axios.get('http://debian:8080/api/orders')
          //axios.get('/api/orders')
            .then(function(response)
            {
              self.orders = response.data;
              self.loading = false;
            })
            .catch(function(error)
            {
              console.log(error);
              self.loading = false;
            })
    },
    showDetails(customerId) {
        this.customerData = null;
        this.customerId = customerId; // this.customerId is a variable, not a function with the samwe name
        this.showDialog = true;
    }
  },

  computed: {
    customerTable: function() {
      var d = this.customerData;
      return [
        {name: 'id', value: d.id},
        {name: 'Company', value: d.company},
        {name: 'Last name', value: d.last_name},
        {name: 'First name', value: d.first_name},
      ];
    }
  },

  watch: { // watch is another reactive field which changes when (customerId in this example) changes
    customerId: function (newId) { // get the data of this customer
      if (!newId) {
        this.customerData = null;
        return;
      }
      var self = this;
      axios.get('http://debian:8080/api/customers' + '/' + newId)
      //axios.get('/api/orders')
        .then(function(response)
        {
          self.customerData = response.data;
          // self.loading = false;
        })
        .catch(function(error)
        {
          console.log(error);
          // self.loading = false;
        })
    }
  }
}
</script>

<style lang="css" scoped>
</style>
