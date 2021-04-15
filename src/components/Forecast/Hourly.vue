<template>

  <div >
      <div :id="darkMode ? 'darkMode-text' : null" class="card-title">
          <div style="padding:1rem">
              <h2 >Hourly Weather - <span  :style="darkMode ? ' color:white;font-weight: 100' : 'color: #000000a1; font-weight: 100'">{{ location }}</span></h2>
                <h3>{{ forecastDate }}</h3>
          </div>
          
     <button class="btn-back" @click="back">Back</button>
      </div>
      
    <div class="hourly-forecast-container">
     <div v-for="(hour,index) in data" :key="hour + index" class="hourly-container" :id="darkMode ? 'darkMode-background' : null">
         <div class="hourly ">
             <span>
                 {{ hour.time.split(" ").slice(1,2).toString().split('').slice(1,2).toString()}} AM
                 </span>
         <span>
             <img src="../../assets/temperature.png" alt="">
             {{ hour.temp_f }}&deg;F
             </span>
         <span><img :src="hour.condition.icon" alt=""></span>
         
         <span><img style="margin-right:10px" src="../../assets/drop.png" alt="precipitation">{{hour.precip_in}}%</span>
        <span><img style="margin-right:10px" src="../../assets/wind.png" alt="wind speed">{{hour.wind_mph}}mph</span>
        <span @click="dropdown(index)">
            <img v-if="index === displayActive  ? true : false" class="chevron" src="../../assets/down-arrow.png">
            <img v-else class="chevron" src="../../assets/up-arrow.png">
            </span>
         </div>
         

            <div  class="hourly-sub hourly" :class="hide ? 'slide-down-sub' : '.slide-up-sub'" :id="darkMode ? 'darkMode-meta' : null"  v-show="index === displayActive">
                <span>
                    <img src="../../assets/windsock.png" alt="">
                    Wind Direction: {{ hour.wind_dir }}
                    </span>
                <span>
                    <img src="../../assets/hot.png" alt="">
                    Feels Like: {{hour.feelslike_f}}&deg;F
                    </span>
                <span>
                    <img src="../../assets/wind_chill.png" alt="">
                    Wind Chill: {{hour.windchill_f}}&deg;F
                    </span>
                <span>
                    <img src="../../assets/humidity.png" alt="">
                    Humidity: {{hour.humidity}}%
                </span>
                <span>
                    <img src="../../assets/snowflake.png" alt="">
                    Chance of Snow: {{hour.chance_of_snow}}%
                    </span>
                <span>
                    <img src="../../assets/rain.png" alt="">
                    Chance of Rain: {{hour.chance_of_rain}}%
                    </span>
                
            </div>

     </div>
    </div>
      
    

     
      
  </div>
</template>

<script>
export default {
    data(){
        return {
            dropdownActive:{
                display: 'flex',
                paddingTop: '1rem', 
                fontSize: '26px',
                lineHeight: '.9',
                listStyleType: 'none',
                justifyContent: 'space-between',
                flexWrap: 'wrap',
            },
            displayActive:Number,
            hide:true
        }
    },
    props:['data','location','forecastDate','darkMode'],
    methods:{
        back(){
            this.$emit('backtoHourly')
        },
        dropdown(index){
            if(this.displayActive !== index){
                this.displayActive = index
                this.hide = true
            }else{
                this.displayActive = null
                this.hide = false
            }
            
            
        }
    }
}
</script>

<style scoped>
.hourly-forecast-container{
    animation: grow 1.5s forwards ease-out;
    overflow: hidden;
    transform-origin: top
}

@keyframes grow {
    from{
        transform: scaleY(0) ;
    }
    to{
        transform:scaleY(1)
    }
}




.card-title{
    display: flex;
    justify-content: space-between;
}

#darkMode-meta{
  background-color: #3e3e3e;
    color: white;
}


.card-title div{
    text-align: left;
    margin-left: 1rem;
}

.card-title button{
    margin-right: 1rem;
}

div{
    width: 100%;
}

.btn-back{
   background: #ffffff00;
    color: #0066ff;
    font-style: italic;
    border: none;
    font-size: 20px;
}

.btn-back:hover{
    color: blue;
}

.chevron{
    cursor: pointer;
}

.hourly-container{
    background-color: #065eb5;
    color: white;
        transform-origin: top;

}

.hourly-sub{
    background-color: white;
    color: black;
    padding-bottom: 1rem;
        transform-origin: top;
        

}

.slide-down-sub{
    animation: slidein .5s ease-out;
}



.hourly-container:nth-child(odd){
    background-color: #bfd9fa;
    color: black;
}



.hourly {
    display: flex;
    padding-top: 1rem; 
    font-size: 26px;
    line-height: .9;
    list-style-type: none;
    justify-content: space-between;
    flex-wrap: wrap;
}

.hourly span{
    padding: .5rem;
    margin-left: 1rem;
    margin-right: 1rem;
}





@keyframes slidein {
      0% {
        transform: scaleY(0);
    }
    100% {
        transform: scaleY(1.0);
    }
}

.input-box {
        display: flex;
        justify-content: space-between;
        margin: 10px;
    }

    @media only screen and (max-width: 532px) {
        .hourly-sub span{
            display: block;
            width: 100%;
            /* border-bottom: solid; */
            background: #4e4e4e;
                }

                .hourly-sub span:nth-child(even){
                    background-color: #333333;
                }
    }
</style>