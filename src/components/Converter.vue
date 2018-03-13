<template>
  <div class="hello">
    <div class="holder">
    <tr>
      <td><input type="number" v-model='amount' @change='rate()' placeholder="0"></td>
      <td><select v-model="currencyfrom" @change='loadData()'>
        <option v-for="(v, k) in currencies" :value='k'>{{k}}</option>
      </select></td>

      <td><span class="fa fa-retweet"></span></td>

      <td><input type="number" placeholder="0" :value='finalAmount'></td>

      <td><select v-model="currencyto" @change='getVal()'>
        <option v-for="(v, k) in currencies" :value='k'>{{k}}</option>
      </select></td>
    </tr>
    <div class="listCur">
      <p v-for="(v, k) in currencies">{{k}} = {{v}}</p>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Converter',
  mounted() {
    this.loadData();
    this.getVal();
  },
  data: () => ({
    currencyfrom: 'EUR',
    currencyto: 'USD',
    amount: '',
    amount2: '',
    currencies: {}
  }),
  methods: {
    loadData() {
      const currencyName = this.currencyfrom;
      axios.get(`http://api.fixer.io/latest?base=${currencyName}`).then(response=>{
        this.currencies = response.data.rates;
        this.currencies[this.currencyfrom] = 1;
        // this.amount2 = response.data.rates[this.currencyto];
      });
    },
    getVal() {
      axios.get('http://api.fixer.io/latest').then(response=>{
        console.log(response.data.rates)
        this.amount2 = response.data.rates[this.currencyto];
      });
    }
  },
  computed: {
    finalAmount: function () {
      let from = this.amount;
      let to = this.amount2;
      let total;

      if (this.currencyfrom != this.currencyto){
        total = (from * to).toFixed(2);
        return total;
      } else {
        return this.amount;
      }
    }
  }


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
    background: #fff;
    padding: 20px;
  }

.holder input {
  border: 1px solid #d3d9de;
  border-radius: 3px;
  width: 103%;
  height: 14px;
}

.holder select {
  border: 1px solid #d3d9de;
}

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  td {
    padding: 10px;
  }

  select {
    width: 60px;
  }

  .listCur p {
    padding: 0px;
    line-height: 0px;
  }
</style>
