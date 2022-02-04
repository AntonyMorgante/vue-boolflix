<template>
    <div id="search-bar">
        <input type="text"
        placeholder="Cerca un film" 
        v-model="searchInput"
        @keyup.enter="searchFilms">
        <button @click="searchFilms">Cerca</button>
    </div>
</template>

<script>
export default {
    name: "SearchBar",
    data(){
        return{
            searchInput:""
        }
    },
    methods:{
        searchFilms: function(){  
            this.$parent.$emit('searchFilms',this.searchInput);
        }
    }
}
</script>

<style>
    #search-bar{
        float:right;
        padding:30px 0;
    }
</style>