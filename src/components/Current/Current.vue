<template>
   <div class="card">

      <h2>{{location.name}}</h2>
      <h3>{{location.region}}</h3>

      <div class="row" style="display:flex; justify-content:space-around">
          <div class="row flex-column">
               <span class="current-temp">{{current.temp_f}}f</span>
               <span>Feels like {{current.feelslike_f}}f </span>
           </div>

           <div class="row flex-column" style="border:none">
               <span class="current-temp"><img width="200" :src="current.condition.icon"  alt=""></span>
           </div>
      </div>

      <div class="flex-row">
          <div class="col-6" style="margin-right:1.5rem">
           

            <div class="row meta-value">
               <span>High/Low</span>
               <span>36/22</span>
           </div>

           <div class="row meta-value">
               <span>Humidity</span>
               <span>36/22</span>
           </div>

           <div class="row" style="padding-top:2rem">
               <button class="btn">Celcius / Fahrenheit</button>
           </div>

       </div>
      <div class="col-6">
           

            <div class="row meta-value">
               <span>Wind</span>
               <span>{{current.wind_mph}}mph</span>
           </div>

           <div class="row meta-value">
               <span>Humidity</span>
               <span>{{current.humidity}}</span>
           </div>

           <div class="row meta-value">
               <span>UV Index</span>
               <span>{{current.uv}}/10</span>
           </div>
       </div>
      </div>

       
    </div>
</template>

<script>
export default {
   
    props:['location','current','forecast'],
    
    created(){
    }
}

</script>

<style scoped>

    .card h2{
        text-align: left;
        font-size: 2rem;
        margin-left: 2rem;
    }

    .card h3{
        margin-left: 2rem;
        text-align: left;
    }

    .row:first-of-type{
        border:none
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

