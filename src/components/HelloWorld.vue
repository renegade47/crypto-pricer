<template>
  <div class="hello">
    <section>
      <div class="tbl-header">
        <table cellpadding="0" cellspacing="0" border="0">
          <thead>
            <tr>
              <th>Coin</th>
              <th>Price in BTC</th>
              <th>Price in USD</th>
              <th>Price in PHP</th>
            </tr>
          </thead>
        </table>
      </div>
      <div class="tbl-content">
        <table cellpadding="0" cellspacing="0" border="0">
          <tbody>
            <tr v-for="(value, key) in cryptos">
              <td>{{ key }}</td>
              <td>{{ value.BTC }} BTC</td>
              <td>${{ value.USD }}</td>
              <td>PHP {{ value.PHP }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
      <div class="footer">
        <p class="credits">Credits to <a href="https://www.cryptocompare.com" target="_blank">cryptocompare</a> for the data</p>
      </div>
  </div>

</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data: () => ({
    cryptos: [],
    errors: []
  }),

  created () {
    axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms=STEEM,SBD,EOS,BTC,ETH,LTC,NEO&tsyms=USD,PHP,BTC')
      .then(response => {
        this.cryptos = response.data
        console.log(response)
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

h1{
  font-size: 30px;
  color: #fff;
  text-transform: uppercase;
  font-weight: 300;
  text-align: center;
  margin-bottom: 15px;
}
table{
  width:100%;
  table-layout: fixed;
}
.tbl-header{
  background-color: rgba(255,255,255,0.3);
 }
.tbl-content{
  height:450px;
  overflow-x:auto;
  margin-top: 0px;
  border: 1px solid rgba(255,255,255,0.3);
}
th{
  padding: 20px 15px;
  text-align: left;
  font-weight: 500;
  font-size: 12px;
  color: #fff;
  text-transform: uppercase;
}
td{
  padding: 15px;
  text-align: left;
  vertical-align:middle;
  font-weight: 300;
  font-size: 12px;
  color: #fff;
  border-bottom: solid 1px rgba(255,255,255,0.1);
}


/* demo styles */

@import url(https://fonts.googleapis.com/css?family=Roboto:400,500,300,700);
body{
  background: -webkit-linear-gradient(left, #283c86, #45a247);
  background: linear-gradient(to right, #283c86, #45a247);
  font-family: 'Roboto', sans-serif;
}
section{
  margin: 50px;
}

/* for custom scrollbar for webkit browser*/

::-webkit-scrollbar {
    width: 6px;
} 
::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
} 
::-webkit-scrollbar-thumb {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
}

.credits {
  text-align: center;
  color: #fff;
}
.credits a {
  color: #fff;
}
</style>
