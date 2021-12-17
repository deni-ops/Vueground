<template>
  <div>
    <a @click="num0++ && num1++ && num2++">Please CLICK_HERE</a><br/><br>
    <input name="num0" v-model="num0"/> <br> <br>
    <!-- data from the table: {{ getData() }} <br/> -->
    num1: {{ num1 }} <br/>
    num2: {{ num2 }} <br />
    <a v-if="num2 == 50">Initial state of num2<br /></a><br>
    {{ mul }}<br><br>

    <el-button><a @click="getData">Show customers</a></el-button><br>
    <el-button><a @click="customers=[]">Hide customers</a></el-button><br><br>


    <!-- spell for printing the table -->
    <table border="2px solid silver" align="center">
      <tr v-for="n in arr" :key="n.key">
        <td><b>Value</b></td>
        <td>{{n}}</td>
      </tr>
    </table>

    <br>

    <table border="1px solid silver" align="center">
      <tr>
        <th>ID</th>
        <th>Last name</th>
        <th>First name</th>
        <th>Company</th>
      </tr>

      <tr v-for="customer in customers" :key="customer.key">
        <td>{{customer.id}}</td>
        <td>{{customer.last_name}}</td>
        <td>{{customer.first_name}}</td>
        <td>{{customer.company}}</td>
      </tr>
    </table>

  </div>
</template>

<script>
import * as _ from 'lodash';
// library for writing http-requests (to DB for instance)
import axios from 'axios';

export default
{
  name: 'Demo2',
  data: function()
  // data is a reactive field which holds all the predefined data
  {
    return {
      num0: 12,
      num1: 45,
      num2: 50,

      customers: [],
    };
  },
  computed:
  // computed is a reactive filed which holds the functions acting on data and maybe props
  {
    mul: function()
    {
      return {
        res1: this.num1*2,
        res2: this.num2*2,
        res3: this.data1,
        res4: this.data2,
      };
    },
    arr: function()
    {
      return _.range(2, this.num0, 2);
    }
  },
  props:
  // props is a reactive field which holds the fileds that later will be filled with values
  {
    data1: Number,
    data2: String,
    data3: Boolean,
    data4: Object,
  },

  methods:
  {
    getData: function ()
    {
      var self = this; // getData() is a specific kind of lambda function (on Russian - замыкание)
      // it cannot resolve the variables marked as 'this', only locally defined variables
      // but 'self' itself is local variable thus we now can resolve 'this' with extra step

      axios.get('http://debian:8080/api/customers')
        .then(function(response) {
          console.log(response);
          self.customers = response.data;
        })
        .catch(function (error) {
          console.log(error);
        })
      // console.log(data);
      // return data;
    }
  }
}

</script>
