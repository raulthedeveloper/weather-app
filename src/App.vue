<template>
  <Main />
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'App',
  components: {
    Main
  }
}
</script>

<style>






 body{
   background-color: #0379ea;
 }

  .container{
    margin-top: 5rem;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    margin-bottom: 5rem;
  }

  .card{
    margin-top: 5rem;
    width: 70%;
    background-color: white;
    display: flex;
    text-align: center;
    flex-direction: column;
    border-radius: 4px;
    padding-bottom: 4rem;
    padding-top: 2rem;
        box-shadow: 1px 7px 31px -3px;
  }

  .row{
    margin-top: .5rem;
    border-top: solid 1px;
  }

  .col-6{
    width: 50%;
  }



  .col-2{
    width: 20%;
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 1rem;
    border-right: solid 1px;
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


</style>
