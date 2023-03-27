<template>
  <div id="app">
    <h3>Register:</h3>
    <small id="nameError" v-show="error">Invalid name</small>
    <br>
    <input type="text" v-model="nameField" placeholder="Name..." id="">
    <br>
    <input type="email" v-model="emailField" placeholder="Email" id="">
    <br>
    <input type="number" v-model="ageField" placeholder="Idade" id="">
    <br>

    <button @click="registerUser">Save</button>
    <h1>Customer Guide</h1>
    <br />
    <div v-for="(c, index) in orderCustomers" :key="c.id">
      <p>{{ index }}</p>
      <Customer :customer="c" :showAge="false" @deleteMe="deleteCustomer($event)" />
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Customer from './components/Customer.vue';
export default {
  name: 'App',
  data() {
    return {
      nameField: "",
      emailField: "",
      ageField: "",
      error: false,
      customers: [
        {
          id: 1,
          name: "Anderson",
          email: "maikbr@gmail.com",
          age: 29
        },
        {
          id: 2,
          name: "Jose",
          email: "jose@gmail.com",
          age: 17
        },
        {
          id: 3,
          name: "Fabio",
          email: "fabio@gmail.com",
          age: 25,
        }
      ]
    }
  },

  components: {
    Customer
  },
  methods: {
    registerUser: function () {
      if (this.nameField == '' || this.nameField == ' ') {
        this.error = true;
      } else {
        this.customers.push({
          id: Date.now(),
          name: this.nameField,
          email: this.emailField,
          age: this.ageField,
          showAge: true
        });
        this.nameField = "";
        this.emailField = "";
        this.ageField = undefined;
      }


    },
    deleteCustomer: function ($event) {
      var id = $event.id;
      var arr = this.customers.filter(c => c.id != id);
      this.customers = arr;
      // $event.component.test();
    }
  }, computed: {
    orderCustomers: function () {
      return _.orderBy(this.customers, ['name'], ['asc']);
    }
  }
}

</script>
<style>
#nameError {
  color: red
}
</style>
