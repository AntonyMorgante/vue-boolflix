<template>
  <main>
      <MovieList :filmAndSeries=filmAndSeries />
  </main>
</template>

<script>
import MovieList from '../sections/MovieList.vue';

export default {
    name: "Main",
    components:{
        MovieList
    },
    props:{
        filmAndSeries: Array,
    }
}
</script>

<style lang="scss" scoped>
    main{
        max-width:1170px;
        margin:0 auto;
    }
</style>