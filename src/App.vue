<template>
  <div id="app">
    <Header @searchFilms="filterCatalog" />
    <Main :filmAndSeries=filmSeries />
  </div>
</template>

<script>
import Main from './components/macro/Main.vue';
import Header from './components/macro/Header.vue';
import axios from "axios";

export default {
  name: 'App',
  components: {
    Main,
    Header
  },
  data(){
    return{
      input: "",
      apiURL: "https://api.themoviedb.org/3/search/",
      films: [],
      series: [],  
    }
  },
  methods:{
    getFilmList: function(){
      axios
        .get((this.apiURL+"movie"), {
          params: {
            api_key: "e99307154c6dfb0b4750f6603256716d",
            query : this.input
          }
        })
        .then((filmList) => {
          this.films = filmList.data.results;
        })
        .catch(function(error){
          console.log(error)
        });
    },
    getSeriesList: function(){
      axios
        .get((this.apiURL+"tv"), {
          params: {
            api_key: "e99307154c6dfb0b4750f6603256716d",
            query : this.input
          }
        })
        .then((seriesList) => {
          this.series = seriesList.data.results;
        })
        .catch(function(error){
          console.log(error)
        });
    },          
    filterCatalog: function(searchInput){
      this.input = searchInput
      this.getFilmList();
      this.getSeriesList();
    }     
  },
  computed: {
    filmSeries (){
      const ObjArray = [];
      this.films.forEach((film)=>{
        const filmObj = {
          title: film.title,
          originalTitle: film.original_title,
          lang: film.original_language,
          rating: film.vote_average,
          poster: film.poster_path
        };
        ObjArray.push(filmObj);
      })
      this.series.forEach((series)=>{
        const seriesObj = {
          title: series.name,
          originalTitle: series.original_name,
          lang: series.original_language,
          rating: series.vote_average,
          poster: series.poster_path
        }
        ObjArray.push(seriesObj);
      })
      return ObjArray;
    },
  }  
}
</script>

<style lang="scss">
body{
  box-sizing: border-box;
  margin:0;
  padding: 0;
  background-color: rgb(44, 37, 37);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
