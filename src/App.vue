<template>
  <div>
  <Headerr/>
  <div class="container">
      
  
    <div class="row">
    <h1> Ethereum  trade </h1>

    <input type="text"
      class="form-control text-light bg-dark rounded-3 border-0 my-4 " 
      placeholder="Searech for Type of Negotiation"
      @keyup="searchDate()"
      v-model="textsearch"
    />
    
      <table class="table table-hover table-dark text-light  "> 
        <thead> 
          <tr>
            <th v-for="(title, index) in titles" :key="index">
              {{title}}
            </th>
          </tr>
        </thead>
          <tbody>
            <tr v-for="(coin, index) in filteredtype" :key="coin.tid">
              <td> <span class="me-3" >{{index + 1}} </span> </td>
              <td>
               <span> {{coin.amount}} </span>
              </td>
              <td> {{ new Date(coin.date * 1000).toLocaleDateString()}} </td>
              <td> R$ {{coin.price.toLocaleString()}} </td>
              <td :class="[coin.type === 'buy' ? 'text-success' : 'text-danger',]"> {{coin.type}} </td>
            </tr>
          </tbody>
      </table>
    </div>
  </div>
  </div>
</template>

<script>
 import Headerr from './components/Headerr.vue'


export default {
  name: 'App',
  components:{
    Headerr
  },
  data() {
    return {
      coin: [],
      filteredtype:[],
      titles: ["*", "Amount", "Date","Unity Price","Type of Negotiation"],
      textsearch: '',
    };
    

  },
  async mounted() {
   const res = await fetch('https://www.mercadobitcoin.net/api/ETH/trades/')
   const data = await res.json()
   console.log(data);
    this.coin = data;
    this.filteredtype= data
  },
    methods: {
      searchDate() {
       this.filteredtype = this.coin.filter((coin) => 
          coin.type.toLowerCase().includes(this.textsearch.toLowerCase()))
        },
    },
    
  
}
</script>


<style >
 * {
    margin: 0;
    padding: 0;
    box-sizing:border-box,
};


</style>