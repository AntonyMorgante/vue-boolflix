<template>
  <li class="poster" :style='{ backgroundImage: `url("${getPoster(poster)}")`}'>
    <div class="hover-details">
      <p>
        <span class="boldtext">Titolo:</span>{{title}}   
      </p>
      <p>
        <span class="boldtext">Titolo originale:</span> {{originalTitle}}
      </p>
      <p>
        <span class="boldtext">Lingua:</span> <img class="flag" :src="setFlag(lang)" alt="">
      </p>
      <p>
        <span class="boldtext">Voto:</span> 
        <img
        v-for="star in getRating(rating)" 
        :key="star"
        class="star"
        src="../../assets/orangestar.png" alt="">      
        <img 
        v-for="star in getEmptyStars(rating)"
        :key="star"
        class="star"
        src="../../assets/greystar.png" alt="">
      </p>
    </div>
  </li>
</template>

<script>
export default {
  name: "Movie",
  props:{
    title: String,
    originalTitle: String,
    lang: String,
    rating: Number,
    poster: String
  },
  methods:{
    setFlag: function(lang){
      let langArray = ["en","it"]
      if (langArray.includes(lang)){
        return require("../../assets/" + lang + ".svg")
      } 
      else {
        return require("../../assets/elselang.svg")
      }
    },
    getPoster(path){
      if (path == null){
        return require("../../assets/noposter.jpg")
      }
      return ("https://image.tmdb.org/t/p/w342/" + path);
    },
    getRating(rating){
      return Math.ceil(rating/2);
    },
    getEmptyStars(rating){
      let n = this.getRating(rating);
      return (5 - n);
    }        
  }
}
</script>

<style>

  .hover-details{
    display: none;
    width:100%;
    height:100%;
    background-color: rgba(0,0,0,0.8);
    font-size:15px;
  }

  li:hover .hover-details{
    display:inline-block;
  }

  .boldtext{
    font-weight: bold;
    padding-right: 2px;
  }

  .flag{
    height:10px;
    width: 15px;
  }

    li{
    flex-basis: 171px;
    margin:10px;
  }

  p{
    padding:0 10px;
  }

  .poster{
    background-size: cover;
    color:white;
    height:250px;
  }

  .star{
    width:15px;
  }
</style>