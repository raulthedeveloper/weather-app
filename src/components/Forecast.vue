<template>
  
     <div class="card">
     
     
     <div class="col-2" v-for="(day, index) in forecast" :key="index">
        <h3>{{day.date}}</h3>
        <span class="forecast-value"> {{day.day.maxtemp_f}}&deg;{{symbol}}</span>
        <span class="&deg;Forecast-value-small">{{day.day.mintemp_f}}&deg;{{symbol}}</span>
        <span class="forecast-value"><img width="60" :src="day.day.condition.icon" alt=""></span>
        <small>Chance of Snow</small>
        <span class="forecast-value">{{day.day.daily_chance_of_snow}}%</span>
      </div>

      
    </div>
    
</template>

<script>
export default {
  data(){
    return {
      symbol:"F",
      measure:"mph"
    }
  },
 props:['current','forecast'],
 created(){
   console.log(this.forecast)
 }
}
</script>

<style scoped>

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
</style>

