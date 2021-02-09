<template>
  <div>
     <ul v-for="(hour,index) in data" :key="hour + index">
         <li>{{hour.time}}</li>
     </ul>
      <button class="btn" @click="back">Back</button>
  </div>
</template>

<script>
export default {
    props:['data'],
    methods:{
        back(){
            this.$emit('backtoHourly')
        }
    }
}
</script>

<style scoped>
.hourly {
    display: flex;
    flex-direction: column;
    padding: 2rem;
    background-color: #e4e4e4;
    margin: 10px;
    color: black;
    border-radius: 6px;
    font-size: 26px;
    line-height: .9;
}

.input-box {
        display: flex;
        justify-content: space-between;
        margin: 10px;
    }
</style>