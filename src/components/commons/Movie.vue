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
        :key=star
        class="star"
        src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a3/Orange_star.svg/300px-Orange_star.svg.png" alt="">      
        <img 
        v-for="star in getEmptyStars(rating)"
        :key="star"
        class="star"
        src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Star_empty.svg/108px-Star_empty.svg.png" alt="">
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
      if (lang == "it"){
        return "https://upload.wikimedia.org/wikipedia/commons/0/03/Flag_of_Italy.svg"
      } else if (lang == "en"){
        return "https://upload.wikimedia.org/wikipedia/en/a/ae/Flag_of_the_United_Kingdom.svg"
      } else {
        return "https://upload.wikimedia.org/wikipedia/commons/9/9e/600px_Grey_HEX-DADADA_with_White_question_mark.svg"
      }
    },
    getPoster(path){
      if (path == null){
        return ("https://fireteller.com/wp-content/uploads/2020/09/Poster_Not_Available2.jpg")
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