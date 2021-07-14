<template>
  <div>
    <div>
      <center>
        <input type="text" ref="searchInput" v-model="search" style="width:330px; margin: auto"/>
      </center>
      <center>
        <md-button style="margin: auto, margin-bottom: 3em" @click="searchMovie()">Search</md-button>
      </center>
    </div>
  </div>
</template>

<script>
  
  export default {
    
    data () {
      return {
        
        search: '',
        title: 'Your Weather',
        forecast: [],
      }       
    },
    methods: {
        searchWeather: function() {
          this.search = this.$refs.searchInput.value;
          // console.log("Search: "+this.search)
          this.$http.get('https://api.themoviedb.org/3/search/movie?api_key=9270421e43cc32ed6056cad8de3c2c67&query=' + this.search ).then(function(data) {
          // console.log("Results: " + data.body)
            this.forecast = data.body.results
          })
       },
      
    }, 
    created() {
    
        this.$http.get('https://api.themoviedb.org/3/movie/popular?api_key=9270421e43cc32ed6056cad8de3c2c67&language=en-US&page='+this.$store.state.currentPage)
        .then(function(data) {
          console.log(data.body.results)
          this.movies = data.body.results
          this.poster = 'https://image.tmdb.org/t/p/w500/'+data.body.results.poster_path
        })
    }, 
    
  }
  
  </script>


<style scoped>

p:hover{
  color: blue;
  text-decoration: none
}
p{
  text-decoration: none

}
li{
    display: inline-block;
    margin: 0 10px;
}

.a{
    color:red;
    text-decoration: none;
    padding: 6px 8px;
    border-radius: 10px;

}

nav{
    background: #444;
    padding: 14px 0;
    margin-bottom: 40px;
}
.router-link-active{
    color:black
}
</style>