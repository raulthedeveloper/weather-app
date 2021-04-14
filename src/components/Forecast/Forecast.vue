<template>
  
     <div class="card" style="padding-top:0;padding-bottom:0;margin-bottom: 4rem;" :style="darkMode ? 'background:#3e3e3e' : null">
       
       <Hourly v-if="hourly" 
       @backtoHourly="back" 
       :data="forecast[currentHourly].hour" 
       :location="location.name"
       :forecastDate="forecast[currentHourly].date"
       :darkMode="darkMode"
       />

     <div v-else class="col-2" :class="darkMode ? 'darkMode': 'lightMode'"  v-for="(day, index) in forecast" :key="index">
        <h3>{{day.date}}</h3>
        <span class="forecast-value"> {{day.day.maxtemp_f}}&deg;{{symbol}}</span>
        <span class="&deg;Forecast-value-small">{{day.day.mintemp_f}}&deg;{{symbol}}</span>
        <span class="forecast-value"><img width="60" :src="day.day.condition.icon" alt=""></span>
        <small>Chance of Snow</small>
        <span class="forecast-value">{{day.day.daily_chance_of_snow}}%</span>

        <button @click="hourlyForecast(index)" class="btn">Hourly</button>
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
      hourly:false,
      currentHourly:0,
    }
  },
 props:['current','forecast','location','darkMode'],
 components:{
   Hourly
 },
 methods:{
   hourlyForecast(index){
     this.hourly = !this.hourly
     this.currentHourly = index
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

.lightMode{
  background-color: #0379ea4a;
  margin: 10px;
}

.lightMode:nth-child(even){
 background-color: #045fb5;
    color: white;
}

.darkMode{
  margin: 10px;
  background-color:  #961d7e;
  color: white;
}

.darkMode:nth-child(even){
  background-color: #5a0d4b;
}




h3{
  font-size: 2rem;
}

  .card{
    flex-direction: row;
    animation: fadeup 2s forwards;
    
  }



  @keyframes fadeup {
    0% {
        opacity: 0;
        -webkit-transform: translateY(90px);
        
    }
    100% {
        opacity: 1;
        
        -webkit-transform: translateY(0);
    }
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

