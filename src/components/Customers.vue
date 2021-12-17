<template>
  <div>
    <h2>Customers</h2>

    <a @click="getData">UPDATE</a> <br/>
    <a @click="customers=[]">RESET</a><br/>

    <table border="1">
      <tr>
        <th>Company</th>
        <th>Last name</th>
        <th>City</th>
      </tr>
      <tr v-for="customer in customers" :key="customer.key">
        <td>{{customer.company}}</td>
        <td>{{customer.last_name}}</td>
        <td>{{customer.city}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default
{
  name: 'Demo',
  data: function() {
      return {
        customers: []
      };
    },
    methods: {
      getData: function() {
          var self = this;
          axios.get('http://debian:8080/api/customers')
          //axios.get('/api/customers') // after proxy in 'vue.config.js' has been added
          .then(function(response)
          {
            console.log(response);
            self.customers = response.data;
          })
          .catch(function(error)
          {
            console.log(error);
          });
        },
    },
}
</script>
