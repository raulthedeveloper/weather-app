<template>

  <div >
      <div class="card-title">
          <div>
              <h2>Hourly Weather - <span style="font-weight: 100;
    color: #000000a1;">{{ location }}</span></h2>
                <h3>{{ forecastDate }}</h3>
          </div>
          
     <button class="btn-back" @click="back">Back</button>
      </div>
      

     <div v-for="(hour,index) in data" :key="hour + index" class="hourly-container">
         <div class="hourly">
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
         

            <div  class="hourly-sub hourly"  v-show="index === displayActive  ? true : false">
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
    props:['data','location','forecastDate'],
    methods:{
        back(){
            this.$emit('backtoHourly')
        },
        dropdown(index){
            if(this.displayActive !== index){
                this.displayActive = index
            }else{
                this.displayActive = null
            }
            
            
        }
    }
}
</script>

<style scoped>
.card-title{
    display: flex;
    justify-content: space-between;
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
    

}

.hourly-sub{
    background-color: white;
    color: black;
    padding-bottom: 1rem;
}

.hourly-container:nth-child(odd){
    background-color: #bfd9fa;
    color: black;
}

.dropdown-hourly {
    display: none;
    
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



.input-box {
        display: flex;
        justify-content: space-between;
        margin: 10px;
    }
</style>