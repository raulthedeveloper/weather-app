<template>
  <div class="container">
   
<Search v-on:changeSearch="updateResult($event)"/>   
<Current 
v-if="!isLoading"
  :location="location"
  :current="current"
  :forecast="forecast"
/>  

<Loading  v-if="isLoading"/>

<Forecast 
v-if="!isLoading"
:current="current"
:forecast="forecast"

/>


    
  </div>
</template>

<script>
import axios from 'axios'
import Search from "./Search.vue"
import Forecast from "./Forecast.vue"
import Current from "./Current/Current.vue"
import Loading from "./Loading.vue"
export default {
  data(){
    return {
      location:null,
      current:null,
      forecast:null,
      isLoading:true,
      search:String
    }
  },
  components:{
    Forecast,
    Current,
    Search,
    Loading
  },

  created() {
      
    
    const options = {
    method: 'GET',
    url: 'http://api.weatherapi.com/v1/forecast.json?key=1590231e5d674493844164905201310&q=18301&days=5',    
  }

      axios.request(options).then((response) => {
        this.location= response.data.location
        this.current = response.data.current
        this.forecast = response.data.forecast.forecastday

        this.isLoading = false
      })
     
  
    },
    updateResult(search){
  //       const options = {
  //      method: 'GET',
  //      url: `http://api.weatherapi.com/v1/forecast.json?key=1590231e5d674493844164905201310&q=${search}&days=5`,    
  // }

  // axios.request(options).then((response) => {
  //       this.location= response.data.location
  //       this.current = response.data.current
  //       this.forecast = response.data.forecast.forecastday

  //       this.isLoading = false
  //     })

     
      console.log(search)
    }
    
    
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 

</style>
