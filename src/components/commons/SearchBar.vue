<template>
    <section id="search-bar">
        <input type="text"
        placeholder="Cerca un film" 
        v-model="searchInput"
        @keyup.enter="$emit(`searchFilms`,searchInput)">
        <button @click="$emit(`searchFilms`,searchInput)">Cerca</button>
    </section>
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
            this.$emit('searchFilms',this.searchInput);
        }
    }
}
</script>

<style>
    #search-bar{
        text-align: center;
    }

    input{
        margin-right: 10px;
    }
</style>