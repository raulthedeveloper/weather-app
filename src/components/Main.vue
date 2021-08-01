<template>


  <div class="container">




    <Search @changeSearch="updateResult($event)" :error="error"  :darkMode="darkMode"/>
    <Current v-if="!isLoading" :location="location" :current="current" :forecast="forecast" :darkMode="darkMode"/>

    <Loading :darkMode="darkMode" v-if="isLoading" />

    <Forecast v-if="!isLoading" :current="current" :forecast="forecast" :location="location" :darkMode="darkMode"/>



  </div>
</template>

<script>
  import axios from 'axios'
  import Search from "./Search.vue"
  import Forecast from "./Forecast/Forecast.vue"
  import Current from "./Current/Current.vue"
  import Loading from "./Loading.vue"


  export default {
    data() {
      return {
        location: null,
        current: null,
        forecast: [],
        isLoading: true,
        search: String,
        error: false,
      }
    },
    components: {
      Forecast,
      Current,
      Search,
      Loading
    },

    props:['darkMode'],

    created() {


      const options = {
        method: 'GET',
        url: 'https://api.weatherapi.com/v1/forecast.json?key=1590231e5d674493844164905201310&q=18301&days=5',
      }

      axios.request(options).then((response) => {
        this.location = response.data.location
        this.current = response.data.current
        this.forecast = response.data.forecast.forecastday
        this.isLoading = false
      }).catch( e => console.log(e))


    },
    methods: {

      updateResult(search) {
        
        this.isLoading = true

        const options = {
          method: 'GET',
          url: `https://api.weatherapi.com/v1/forecast.json?key=1590231e5d674493844164905201310&q=${search}&days=5`,
        }

       
          axios.request(options).then((response) => {
            
           if (response.status === 200) {
             
            this.search = search
            this.location = response.data.location
            this.current = response.data.current
            this.forecast = response.data.forecast.forecastday
            this.isLoading = false
            this.error = false
          }
          


        })
        .then(() =>{
           this.isLoading = false
            
        }).catch(e => {
          console.log(e)
          this.error = true
          this.isLoading = false
        })
        
        


      }
    }



  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>







</style>