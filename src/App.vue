<template>
<div :class="darkMode ? 'darkMode-body' : 'lightMode-body'">


<div class="container" style="margin:0; ">
  <span  :style="'margin-top:2rem; color:white'">
    Dark Mode
  </span>
 
<label class="switch">
  <input type="checkbox" @click="toggleDarkMode" :checked="darkMode">
  <span class="slider round"></span>
</label>
</div>

  <Main :darkMode="darkMode"/>
</div>

</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  },
  mounted(){
    if(localStorage.getItem('darkMode') === null){
      localStorage.setItem('darkMode',JSON.stringify(false))
    }else{
       localStorage.setItem('darkMode',JSON.stringify(this.darkMode))
    }
   
  },
  data(){
    return {
      darkMode:JSON.parse(localStorage.getItem('darkMode'))
    }
  },
  methods:{
    toggleDarkMode(){
      this.darkMode = !this.darkMode
       localStorage.setItem('darkMode',JSON.stringify(this.darkMode))
        console.log(JSON.parse(localStorage.getItem('darkMode')))
    }
  }
}
</script>

<style>
*{
  margin: 0;
}
#app{
  height: 100vh;
}

#darkMode-text{
    color: white;
}

#darkMode-background{
  background-color:  #961d7e;
  color: white;

}

#darkMode-background:nth-child(even){
background-color: #5a0d4b;
}



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
  background-color: #961d7e;
}

input:focus + .slider {
  box-shadow: 0 0 1px #961d7e;
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


.darkMode-body{
  background-color: #1c1f21;
  
}




 .lightMode-body{
   background-color: #0379ea;
  padding-bottom: 3rem;
 }

  .container{
    margin-top: 1rem;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    margin-bottom: 5rem;
  }

  .card{
    margin-top: 2rem;
    width: 70%;
    background-color: white;
    display: flex;
    text-align: center;
    flex-direction: column;
    border-radius: 4px;
    padding-bottom: 2rem;
    padding-top: 2rem;
    box-shadow: 1px 7px 31px -3px;
   
  }

   @media only screen and (max-width: 750px) {
   .card{
     width:100%;
     box-shadow: none;
   }
   .container{
     margin-top: 2rem;
   }
 }

  .row{
    margin-top: .5rem;
  }

  .col-6{
    width: 50%;
  }



  .col-2{
    width: 30%;
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 1rem;
  }

  .btn{
    color: white;
    background: #29b529;
    border: none;
    padding: .5rem;
    border-radius: 2px
  }

  .btn:hover{
    background:#197319;
  }
  .btn:active{
    background: #145d14;
  }


.fade-down{
    animation: fadedown 1s forwards ease-out;

}

@keyframes fadedown {
    0% {
        opacity: 0;
        -webkit-transform: translateY(-40px);
    }
    100% {
        opacity: 1;
        -webkit-transform: translateY(0);
    }
}


.fade-up{
    animation: fadeup 1s forwards ease-out;

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




.fade-in{
    animation: fadein 1.5s forwards ease-out;

}

@keyframes fadein {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}




    
    .slide-col .meta-value{
       
        animation: slidein 0.5s forwards ease-out ;
        transform-origin: 50% 0%;
    }

.slide-out-col .meta-value{
       
        animation: slideout 0.5s forwards ease-out ;
        transform-origin: 50% 0%;
    }

 .slide-col .darkMode-meta-value{
       
        animation: slidein 0.5s forwards ease-out ;
        transform-origin: 50% 0%;
    }

.slide-out-col .darkMode-meta-value{
       
        animation: slideout 0.5s forwards ease-out ;
        transform-origin: 50% 0%;
    }




.slide-in{
   animation: slidein 0.5s forwards ease-out ;
  transform-origin: 50% 0%;
}

.slide-out{
       animation: slideout 0.5s forwards ease-out ;
  transform-origin: 50% 0%;
}
   


    @keyframes slidein {
      0% {
        transform: scaleY(0);
    }
    100% {
        transform: scaleY(1.0);
    }
}

@keyframes slideout {
      0% {
        transform: scaleY(1.0);
    }
    100% {
        transform: scaleY(0);
    }
}

</style>
