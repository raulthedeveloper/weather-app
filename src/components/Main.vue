<template>


  <div class="container">

<div style="display:flex; flex-direction:column; justify-content:center">
  <span style="margin-bottom:.5rem">
    Dark Mode
  </span>
     
<label class="switch">
  <input type="checkbox">
  <span class="slider round"></span>
</label>
</div>



    <Search @changeSearch="updateResult($event)" :error="error"  />
    <Current v-if="!isLoading" :location="location" :current="current" :forecast="forecast" />

    <Loading v-if="isLoading" />

    <Forecast v-if="!isLoading" :current="current" :forecast="forecast" :location="location" />



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
        darkMode:false
      }
    },
    components: {
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
          url: `http://api.weatherapi.com/v1/forecast.json?key=1590231e5d674493844164905201310&q=${search}&days=5`,
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
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  margin-bottom: 1.5rem;
}

.switch input { 
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

</style>