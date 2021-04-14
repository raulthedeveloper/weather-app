<template>
   <div class="card fade-up" :style="darkMode ? 'background:#3e3e3e' : null">

      <h2 :id="darkMode ? 'darkMode-text' : null">{{location.name}}</h2>
      <span class="current-sub-title" :id="darkMode ? 'darkMode-text' : null">{{location.region}}</span>
      <span class="current-sub-title" :id="darkMode ? 'darkMode-text' : null">{{forecast[0].date}}</span>
      

      <div class="row main-display">
          <div class="row flex-column">
               <span class="current-temp fade-in" :id="darkMode ? 'darkMode-text' : null">{{current.temp_f}}&deg;{{symbol}}</span>
               <span :id="darkMode ? 'darkMode-text' : null">Feels like {{current.feelslike_f}}&deg;{{symbol}}</span>
           </div>

           <div class="row flex-column" style="border:none">
               
                   <img width="200" class="fade-in" :src="current.condition.icon.replace('64x64','128x128')"  alt="">
                
                         
           </div>
      </div>

      <div class="flex-row fade-down">
          <div class="col-6">
           

            <div class="row " :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>High/Low</span>
               <span>{{forecast[0].day.mintemp_f}}&deg;{{symbol}} / {{forecast[0].day.maxtemp_f}}&deg;{{symbol}}</span>
           </div>

           <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Barometer</span>
               <span>{{ current.pressure_in}} inHg</span>
           </div>
            
           <div v-if="seeMore" :class="seeMore ? 'slide-col' : 'slide-out-col'">
               <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>UV Index</span>
               <span>{{current.uv}}/10</span>
           </div>

           <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Sun Rise</span>
               <span>{{forecast[0].astro.sunrise}}</span>    
              </div>

              <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Moon Rise</span>
               <span>{{forecast[0].astro.moonrise}}</span>    
              </div>

              <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Chance of Snow</span>
               <span>{{forecast[0].day.daily_chance_of_snow}}%</span>    
              </div>

          </div>

       </div>
      <div class="col-6">
           

            <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Wind</span>
               <span>{{current.wind_mph}} {{measure}} / {{current.wind_dir}}</span>
           </div>

           <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Humidity</span>
               <span>{{current.humidity}}%</span>
           </div>

          <div v-if="seeMore" :class="slideDown < 2 ? 'slide-col' : null">

               <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Moon Phase</span>
               <span>{{forecast[0].astro.moon_phase}}</span>    
              </div>

              <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Sun Set</span>
               <span>{{forecast[0].astro.sunset}}</span>    
              </div>

              <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Moon Set</span>
               <span>{{forecast[0].astro.moonset}}</span>    
              </div>

              <div class="row" :class="darkMode ? 'darkMode-meta-value' : 'meta-value'">
               <span>Chance of Rain</span>
               <span>{{forecast[0].day.daily_chance_of_rain}}%</span>    
              </div>
          </div>
       </div>
      </div>

       <div class="row" style="padding-top:2rem;">
               <button class="btn fade-in" @click="seeMoreToggle">{{!seeMore ? 'See More' : 'See Less'}}</button>
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
            weather:String,
            slideDown:0
        }
    },
   
   
    props:['location','current','forecast','darkMode'],

    methods:{
        seeMoreToggle(){
            this.seeMore = !this.seeMore
            // if(this.slideDown < 2){
            //     this.slideDown+=1
            // }
            
        }
    }
   
   
}

</script>

<style scoped>



.current-sub-title{
    font-size: 1rem;
    text-align: left;
    margin-left: 2rem;
    color: #000000a6;
    margin-top: 1rem;
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
        flex-wrap: wrap;
    }





    .meta-value{
        justify-content: space-around;
        display: flex;
        padding-top: 2rem;
        padding-bottom: 2rem;
        margin-left: 10px;
        margin-right: 10px;
        margin-bottom: 10px;
        background-color: #0379ea4a;
    }
    .meta-value:nth-child(even){
        background-color:#045fb5;
        color: white;
    
    }

    .darkMode-meta-value{
        justify-content: space-around;
        display: flex;
        padding-top: 2rem;
        padding-bottom: 2rem;
        margin-left: 10px;
        margin-right: 10px;
        margin-bottom: 10px;
        background-color: #961d7e;
        color:white;
    }

    .darkMode-meta-value:nth-child(even){
        background-color: #5a0d4b;
    }

    .darkMode-meta-value span{
        font-size: 1.3rem;
    }

    .meta-value span:first-of-type{
        font-weight: bold;
    }

    .meta-value span{
        font-size: 1.3rem;
    }

    .btn{
        width: 10rem;
        font-size: 22px;
    }

    .main-display{
        display:flex; 
        justify-content:space-around; 
        flex-wrap:wrap-reverse
    }

    @media only screen and (max-width: 800px) {

        .col-6{
            flex-direction: column;
        }
  
}

 @media only screen and (max-width: 600px) {
     .col-6{
         width: 100%;
     }
     .meta-value{
         flex-direction: column;
     }

    .main-display{
    flex-wrap: wrap-reverse;
    flex-direction: column-reverse;
    align-items: center;
    margin-bottom: 2rem;
    }
 }

 
</style>

