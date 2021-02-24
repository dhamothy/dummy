<template>
  <div id="app">
    <div id="nav">
      <input type="text" v-model="search" placeholder="Search...">
      <div v-for="data in getData" :key="data.name">
        <div>{{ data.name }}</div>        
        <div>{{ data.gender }}</div>
        <div>{{ data.birth_year }}</div>
      </div>      
    </div>    
    <router-view/>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  data(){
    return{
      datas: [],           
      search: ''
    }
  },
  methods:{
    
  },
  mounted(){    
    axios.get('https://swapi.dev/api/people/').then(response =>{
      this.datas = response.data.results;           
    })    
  },
  computed:{
    getData(){      
      return this.datas.filter( data => {
        return data.name.toLowerCase().includes(this.search.toLowerCase())
      });      
    }
  }
}
</script>

<style lang="scss">
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;  
  max-width: 1000px;
  margin: 40px auto;
  color: #2c3e50;
}
#nav{
  [type="text"]{
    width:100%;
    border:1px solid #aaa;   
    padding: 12px 20px;  
    font: inherit;
    margin-bottom: 20px;
  }
  >div{
    display:flex;     
    padding: 12px; 
    border-bottom: 1px solid #ddd;
    >div{
      flex: 1;
    }
  }
}
</style>
