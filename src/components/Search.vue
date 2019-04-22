<template>
<div id="search">
  <h2> Search Github Users</h2>
  <div class="search-input">
  <el-input v-model="input" placeholder="请输入要查询的ID"><el-button slot="append" icon="el-icon-search" @click="search"></el-button></el-input>
  </div>
</div>
</template>

<script>
import PubSub from 'pubsub-js'
export default {
  name: 'Search',
  data () {
    return {
      input: ''
    }
  },
  methods: {
    search () {
      const search = this.input.trim()
      if (search) {
        PubSub.publish('search', search)
      } else {
        this.$message({
          message: '请输入有效值',
          type: 'warning'
        })
      }
    }
  }
}
</script>

<style scoped>
  #search{
    width: 80%;
    height: 200px;
    min-width: 500px;
    margin: 30px auto;
    background-color: wheat;
    border-radius: 50px;
  }

  #search > h2 {
    padding: 40px 100px 0 100px;
  }

  #search > .search-input{
    padding: 0 100px;
  }

</style>
