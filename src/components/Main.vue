<template>
  <div class="container">
   
<Current 
v-if="!isLoading"
  :location="location"
  :current="current"
  
  
/>  

<Forecast 
v-if="!isLoading"
:current="current"
:forecast="forecast"

/>


    
  </div>
</template>

<script>
import axios from 'axios'
import Forecast from "./Forecast.vue"
import Current from "./Current/Current.vue"
export default {
  data(){
    return {
      location:null,
      current:null,
      forecast:null,
      isLoading:true
    }
  },
  components:{
    Forecast,
    Current
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

        console.log(response.data)

        this.isLoading = false
      })
     
  
    }
    
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 

</style>
