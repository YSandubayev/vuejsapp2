<template>
    <div>
      <button v-on:click="sendEmoji('normal')">Normal 😃</button>
      <button v-on:click="sendEmoji('good')">Good 😍</button>
      <button v-on:click="sendEmoji('bad')">Bad 😎</button>
    </div>
</template>
  
  <script>
  import axios from 'axios'
  export default {
    name: 'ShopVue',
    data() {
      return {
        modifiedData: {
          status: '',
          ip_address: '',
          shop_id: this.$route.params.id
        },
        error: null
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