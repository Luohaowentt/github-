<template>
<div id="user-main">
  <h2  v-if="firstView">输入用户名搜索</h2>
  <h2 v-if="loading">Loading...</h2>
  <h2 v-if="!errMsg"></h2>
  <div class="user" v-for="(user,index) in users" :key="index">
    <a :href="user.url">
      <img :src="user.img_url" style="width: 150px">
    </a>
    <p>{{user.name}}</p>
  </div>
</div>
</template>

<script>
import PubSub from 'pubsub-js'
import axios from 'axios'
export default {
  name: 'Main',
  data () {
    return {
      firstView: true,
      loading: false,
      errMsg: '',
      users: null // user.url,user.img_url,user.name
    }
  },
  mounted () {
    PubSub.subscribe('search', (msg, search) => {
      const url = `https://api.github.com/search/users?q=${search}`
      this.users = null
      this.errMsg = ''
      this.firstView = false
      this.loading = true
      axios.get(url).then(response => {
        const result = response.data
        console.log(result)
        const users = result.items.map(item => ({
          url: item.html_url,
          img_url: item.avatar_url,
          name: item.login
        }))
        this.loading = false
        this.users = users
      }).catch(error => {
        this.errMsg = error
      })
    })
  }
}
</script>

<style scoped>
  #user-main{
    display: flex;
    flex-wrap: wrap;
    margin: 20px auto;
    width: 85%;
    min-width: 1000px;
  }

  .user{
    float: left;
    width: 250px;
    height: 200px;
    border: 1px solid whitesmoke;
    margin: 10px 0;
    background-color: beige;
    text-align: center;
  }

</style>
