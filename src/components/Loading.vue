<template>
<div class="lightMode-body" :id="darkMode ? 'darkMode' : null">
   <img src="../load-spinner.gif" alt="loading spinner">
</div>
</template>

<script>
export default {
    props:['darkMode']
}
</script>

<style scoped>

.lightMode-body{
    background: white;
    border-radius: 5px;
    min-height: 300px;
    display: flex;
    width: 70%;
    margin: auto;
    height: 100vh;
}

img{
    display: block;
    margin: auto;
}

#darkMode{
background-color: #3e3e3e;

}

@media only screen and (max-width: 750px) {
    div{
        width: 100%;
        min-height: 80vh;
    }
}
</style>