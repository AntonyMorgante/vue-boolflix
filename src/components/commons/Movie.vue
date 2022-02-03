<template>
  <li>
    <p>
      <span class="boldtext">Titolo:</span>{{title}}   
    </p>
    <p>
      <br><span class="boldtext">Titolo originale:</span> {{originalTitle}}
    </p>
    <p>
      <br><span class="boldtext">Lingua:</span> {{lang}}
    </p>
    <p>
      <br><span class="boldtext">Voto:</span> {{rating}}
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
    rating: Number
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

  p{
    padding-left: 30px;
    padding-right: 30px;
  }

  .boldtext{
    font-weight: bold;
  }
</style>