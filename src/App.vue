<template>
  <h2>Please, choose the shop which you visited and rate our service</h2>
  
   <div id="app">
    <button v-on:click="sendEmoji('normal')">Normal 😃</button>
    <button v-on:click="sendEmoji('good')">Good 😍</button>
    <button v-on:click="sendEmoji('bad')">Bad 😎</button>
   </div>

   <!-- { path: '/product/:id', component: Product },
   { path: '/shop/:id', component: Shop },
   { path: '/product/:id', component: () => import('../views/Product.vue') }, -->
 
  <!-- <div id="nav">
    <router-link to="/shops/1" @click.prevent>Mega</router-link> |
    <router-link to="/shops/2" @click.prevent>Mega Moskva</router-link>
  </div> -->
<router-view/>

</template>

<script>
import axios from 'axios';
// import Mega from './components/Mega.vue';
// import MegaMoskva from './components/MegaMoskva.vue';
export default {
  name: 'App',
  // components: {
  //   Mega,
  //   MegaMoskva
  // },
  data() {
    return {
      feedbacks: [],
      modifiedData: {
          status: '',
          ip_address: '',
          shop_id: this.$route.params.id
        },
      error: null
    }
  },

  async mounted () {
    try {
      const response = await axios.get('https://immense-wave-26764.herokuapp.com/api/shops')
      this.feedbacks = response.data;
    } catch (error) {
      this.error = error;
    }
  },

methods: {
    sendEmoji(status) {
      axios.post('https://immense-wave-26764.herokuapp.com/api/feedbacks', {
        data: {
            status: status, //modifiedData.status,
            ip_address: '126.12.29.29', //modifiedData.ip_address,
            shop_id: this.$route.params.id //modifiedData.shop_id
          }
        })
        .then(response => {
          console.log(response.data)
        })
        .catch(error => {
          console.error(error)
        })
    }


  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
