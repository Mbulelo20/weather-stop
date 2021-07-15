<template>
  <div>
    <div>
      <center>
        <input type="text" ref="searchInput" v-model="search" style="width:330px; margin: auto"/>
      </center>
      <center>
        <button style="margin: auto, margin-bottom: 3em" @click="searchCity()">Search</button>
      </center>
    </div>
    <div v-for="c in city" :key="c.id">
        <h5>
            {{c.place_name}}
        </h5>
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
        city: ''
      }       
    },
    methods: {
        searchCity: function() {
          this.city = this.$refs.searchInput.value;
            console.log("Search: "+this.city)
        this.$http.get('https://api.mapbox.com/geocoding/v5/mapbox.places/'+this.city+'.json?access_token=pk.eyJ1IjoibWJ1bGVsbyIsImEiOiJja25rN2pxbGIwOGR3MnZvMHZhbm04c3dlIn0.D1L9umIswRGLIgDh0BpSYg')
        .then(function(data) {
        //   console.log(data.body.features[0].place_name)
          console.log(data.body)

          this.city = data.body.features
        })
       },
      
    }, 
    created() {
    
        
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