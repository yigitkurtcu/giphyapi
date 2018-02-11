<template>
  <div id="app">
    <search v-on:SearchRequested="handleSearch"></search>
        <p v-if="isLoading">Loading</p>
    <preview v-bind:gifs=gifs></preview>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Preview from './components/Preview.vue'
export default {
  name: 'app',
  components:{Search, Preview},
  data(){
    return {
      isLoading: true,
      gifs:[]
    }
  },
  methods:{

    doQuery(url){
      fetch(url)
      .then((res) => {return res.json()})
      .then((res) => {
      this.gifs = res.data;
      this.isLoading = false;
      })
    },

    handleSearch(query){
      this.gifs = [];
      this.isLoading=true;
      const url = `http://api.giphy.com/v1/gifs/search?api_key=3QWGzYR37i36hbpwYli87YJsLPZOJlT2&q=${query}&limit=30`;
      this.doQuery(url);
      }
  },

  created(){
    const url = `http://api.giphy.com/v1/gifs/trending?api_key=3QWGzYR37i36hbpwYli87YJsLPZOJlT2&limit=30`;
    this.doQuery(url);
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  background-color:#04051b
}
</style>
