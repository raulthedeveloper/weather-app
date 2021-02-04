<template>
   <div class="card">

      <h2>{{location.name}}</h2>
      <span class="current-sub-title">{{location.region}}</span>
      <span class="current-sub-title">{{forecast[0].date}}</span>
      

      <div class="row" style="display:flex; justify-content:space-around">
          <div class="row flex-column">
               <span class="current-temp">{{current.temp_f}}&deg;{{symbol}}</span>
               <span>Feels like {{current.feelslike_f}}&deg;{{symbol}}</span>
           </div>

           <div class="row flex-column" style="border:none">
               
                   <img width="200" :src="current.condition.icon.replace('64x64','128x128')"  alt="">
                   

              
               
           </div>
      </div>

      <div class="flex-row">
          <div class="col-6" style="margin-right:1.5rem">
           

            <div class="row meta-value">
               <span>High/Low</span>
               <span>{{forecast[0].day.mintemp_f}}&deg;{{symbol}} / {{forecast[0].day.maxtemp_f}}&deg;{{symbol}}</span>
           </div>

           <div class="row meta-value">
               <span>Barometer</span>
               <span>{{ current.pressure_in}} inHg</span>
           </div>
            
           <div v-if="seeMore">
               <div class="row meta-value">
               <span>UV Index</span>
               <span>{{current.uv}}/10</span>
           </div>

           <div class="row meta-value">
               <span>Sun Rise</span>
               <span>{{forecast[0].astro.sunrise}}</span>    
              </div>

              <div class="row meta-value">
               <span>Moon Rise</span>
               <span>{{forecast[0].astro.moonrise}}</span>    
              </div>

              <div class="row meta-value">
               <span>Chance of Snow</span>
               <span>{{forecast[0].day.daily_chance_of_snow}}%</span>    
              </div>

          </div>

       </div>
      <div class="col-6">
           

            <div class="row meta-value">
               <span>Wind</span>
               <span>{{current.wind_mph}} {{measure}} / {{current.wind_dir}}</span>
           </div>

           <div class="row meta-value">
               <span>Humidity</span>
               <span>{{current.humidity}}%</span>
           </div>

          <div v-if="seeMore">

               <div class="row meta-value">
               <span>Moon Phase</span>
               <span>{{forecast[0].astro.moon_phase}}</span>    
              </div>

              <div class="row meta-value">
               <span>Sun Set</span>
               <span>{{forecast[0].astro.sunset}}</span>    
              </div>

              <div class="row meta-value">
               <span>Moon Set</span>
               <span>{{forecast[0].astro.moonset}}</span>    
              </div>

              <div class="row meta-value">
               <span>Chance of Rain</span>
               <span>{{forecast[0].day.daily_chance_of_rain}}%</span>    
              </div>
          </div>
       </div>
      </div>

       <div class="row" style="padding-top:2rem;">
               <button class="btn" @click="seeMore = !seeMore">{{!seeMore ? 'See More' : 'See Less'}}</button>
           </div>
    </div>
</template>

<script>
export default {
   
    data(){
        return {
            symbol:"F",
            measure:"mph",
            seeMore:false,
            weather:String
        }
    },
   
   
    props:['location','current','forecast'],
   
   
}

</script>

<style scoped>

.current-sub-title{
    font-size: 1rem;
    text-align: left;
    margin-left: 2rem;
    color: #000000a6;
}

    .card{
        margin-top: 0;
    }
    .card h2{
        text-align: left;
        font-size: 2rem;
        margin-left: 2rem;
        line-height: 0;
    }

    .card h3{
        margin-left: 2rem;
        text-align: left;
    }

    

    

    .current-temp{
        font-size: 6rem;
        text-align: left;
    }
    .flex-column{
        display: flex;
        flex-direction: column;
        
    }

    .flex-row{
        display: flex;
        flex-direction: row;
    }

    .meta-value{
        justify-content: space-around;
        display: flex;
        padding-top: 2rem;
        padding-bottom: 2rem;
            border-top: solid 1px
    }

    .meta-value span:first-of-type{
        font-weight: bold;
    }

    .meta-value span{
        font-size: 1.3rem;
    }

    @media only screen and (max-width: 800px) {

        .col-6{
            width: 100%;
            flex-direction: column;
        }
  
}

 
</style>

