<template>
  <header>
    <div class="clearfix container">
      <h1>Boolfix</h1>
      <SearchBar />
    </div>
  </header>
</template>

<script>
import SearchBar from "../commons/SearchBar.vue";

export default {
    name: "Header",
    components:{
      SearchBar
    },
}
</script>

<style>
  header{
    background-color:red;
    position: static;
    top:0;
    left:0;
    width:100%;
    height:80px;
  }

  .container{
    max-width:1170px;
    margin: 0 auto;
  }

  h1{
    float:left;
    text-transform: uppercase;
  }

  .clearfix::after{
    content:"";
    display:table;
    clear:both;
  }
</style>