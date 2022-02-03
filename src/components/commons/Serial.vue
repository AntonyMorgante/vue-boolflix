<template>
  <li>
    <div>
        <img class="poster" :src="getPoster(poster)" alt="">
    </div>
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
    getPoster(poster){
        return ("https://image.tmdb.org/t/p/w342/" + poster);
    },
    getRating(rating){
      return Math.floor(1+(rating/2));
    },
    getEmptyStars(rating){
      let n = this.getRating(rating);
      return (5 - n);
    }
  }
}
</script>

<style>
  li{
    flex-basis: calc(100% / 5);
    margin: 20px;
    border: 1px solid black;
    background-color: white;
  }

  p,
  div{
    padding: 10px 30px;
  }


  .boldtext{
    font-weight: bold;
    padding-right: 2px;
  }

  .poster{
    width:100%;
    height: 430px;
  }

  .flag{
    height:15px;
    width: 20px;
  }

  .star{
    width:15px;
  }
</style>