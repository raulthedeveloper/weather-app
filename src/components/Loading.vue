<template>
<div>
   <img src="../load-spinner.gif" alt="">

</div>
</template>



<style scoped>

div{
    background: white;
    border-radius: 5px;
    min-height: 300px;
    display: flex;
    width: 70%;
}
img{
    display: block;
    margin: auto;
}

@media only screen and (max-width: 750px) {
    div{
        width: 100%;
        min-height: 80vh;
    }
}
</style>