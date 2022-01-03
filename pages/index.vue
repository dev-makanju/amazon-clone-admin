<template>
  <Tutorial :products="products"/>
</template>

<script>
//import axios from 'axios'
export default {
    //asynData is fetching data befor the page load ,this is possible omly in nuxt js
    //it's good for seo optimisation
  async asyncData({ $axios }){
    try{
      let response = await $axios.$get("http://localhost:5000/api/products");
      console.log(response);
      return{
         products:response.products
      }
    }catch(err){
       console.log(err)
    }
    }
  }
</script>
