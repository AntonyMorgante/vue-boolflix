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
      />
    </ul>
  </section>

</template>

<script>
import SearchBar from "../commons/SearchBar.vue";
import Movie from "../commons/Movie.vue";
import axios from "axios";

export default {
    name:"MovieList",
    data(){
      return{
        apiURL: "https://api.themoviedb.org/3/search/movie",
        films: [],
        input:"0"
      }
    },
    components:{
      SearchBar,
      Movie
    },
    methods:{
      getFilmList: function(){
        axios
          .get(this.apiURL, {
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
      filterCatalog: function(searchInput){
        this.input = searchInput;
        this.getFilmList();
      }      
    },
    created(){
      this.getFilmList();
    },
    computed: {
        filteredFilms(){
          return this.films;
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