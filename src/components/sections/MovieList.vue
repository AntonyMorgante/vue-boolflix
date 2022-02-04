<template>
  <ul>
    <Movie v-for="(elem,index) in filmAndSeries" 
    :key="index"
    :title=elem.title
    :originalTitle=elem.originalTitle
    :lang=elem.lang
    :rating=elem.rating
    :poster=elem.poster
    />    
  </ul>
</template>

<script>
import Movie from "../commons/Movie.vue";

export default {
    name:"MovieList", 
    components:{
      Movie
    },
    props:{
      filmAndSeries:Array
    }
}
</script>

<style>
  ul{
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    list-style-type: none;
    padding: 0;
  }
</style>