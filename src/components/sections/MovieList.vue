<template>
  <section>
    <SearchBar @searchFilms="filterCatalog" />
    <ul>
      <Movie v-for="(film,index) in filteredFilms" 
      :key="index"
      :title=film.title
      :originalTitle=film.original_title
      :lang=film.original_language
      :rating=film.vote_average
      :poster=film.poster_path
      />
      <Serial v-for="(serial,index) in filteredSeries" 
      :key="index"
      :title=serial.name
      :originalTitle=serial.original_name
      :lang=serial.original_language
      :rating=serial.vote_average
      :poster=serial.poster_path
      />      
    </ul>
  </section>

</template>

<script>
import SearchBar from "../commons/SearchBar.vue";
import Movie from "../commons/Movie.vue";
import Serial from "../commons/Serial.vue";
import axios from "axios";

export default {
    name:"MovieList",
    data(){
      return{
        apiURL: "https://api.themoviedb.org/3/search/",
        films: [],
        series: [],
        input:""
      }
    },
    components:{
      SearchBar,
      Movie,
      Serial
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
        this.input = searchInput;
        this.getFilmList();
        this.getSeriesList();
      }      
    },
    computed: {
        filteredFilms(){
          return this.films;
        },
        filteredSeries(){
          return this.series;
        }

    }
}
</script>

<style>
  ul{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    list-style-type: none;
  }
</style>