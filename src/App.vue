<template>
  <div id="app">
    <Search/>
    <Main/>
  </div>
</template>

<script>

import Search from '@/components/Search'
import Main from '@/components/Main'
export default {
  name: 'App',
  components: {
    Main,
    Search
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  margin-top: 60px;
}
</style>
