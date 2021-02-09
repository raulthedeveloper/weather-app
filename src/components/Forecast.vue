<template>
  
     <div class="card">
       <Hourly v-if="hourly" @backtoHourly="back" :data="forecast.hour"/>
     <div v-else class="col-2" v-for="(day, index) in forecast" :key="index">
        <h3>{{day.date}}</h3>
        <span class="forecast-value"> {{day.day.maxtemp_f}}&deg;{{symbol}}</span>
        <span class="&deg;Forecast-value-small">{{day.day.mintemp_f}}&deg;{{symbol}}</span>
        <span class="forecast-value"><img width="60" :src="day.day.condition.icon" alt=""></span>
        <small>Chance of Snow</small>
        <span class="forecast-value">{{day.day.daily_chance_of_snow}}%</span>
        <button @click="hourlyForecast" class="btn">Hourly</button>
      </div>

      
    </div>
    
</template>

<script>
import Hourly from './Hourly.vue'

export default {
  data(){
    return {
      symbol:"F",
      measure:"mph",
      hourly:false
    }
  },
 props:['current','forecast'],
 components:{
   Hourly
 },
 methods:{
   hourlyForecast(){
     this.hourly = !this.hourly
   },
   back(){
     this.hourly = false
   }
 }
}
</script>

<style scoped>
  .btn{
    margin-top: 1rem;
  }

.col-2{
  background-color: #0379ea4a;
  margin: 10px;
}

.col-2:nth-child(even){
 background-color: #045fb5;
    color: white;
}

h3{
  font-size: 2rem;
}

  .card{
    flex-direction: row;
  }

  .forecast-value{
    font-size: 2.2rem;
  }

  .forecast-value-small{
    font-size: 1.7rem;
    color: #000000a6;
  }

    @media only screen and (max-width: 600px) {
      .card{
       flex-direction: column;
       align-items: center;
  }
  .col-2{
    width: 90%;
  }
    }
</style>

