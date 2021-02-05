<template>
    <div class="input-container">
        <div class="input-box">
            <div>
                <input @keyup.enter="appSearch" type="text" placeholder="enter city or zip" v-model="search">
                <button class="btn" @click="appSearch">Search</button>
            </div>

            <span v-if="error" class="no-result">No Result</span>

           
        </div>
        <div v-if="results">
            <div class="searchList">
            <span>Florida</span>
            <span>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Officiis dignissimos vel repellat atque reprehenderit itaque nobis optio. Ab id laboriosam eligendi quasi esse soluta error ex, consequatur quia accusantium commodi.</span>
        </div>

        <div class="searchList">
            <span>Florida</span>
            <span>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Officiis dignissimos vel repellat atque reprehenderit itaque nobis optio. Ab id laboriosam eligendi quasi esse soluta error ex, consequatur quia accusantium commodi.</span>
        </div>

        <div class="searchList">
            <span>Florida</span>
            <span>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Officiis dignissimos vel repellat atque reprehenderit itaque nobis optio. Ab id laboriosam eligendi quasi esse soluta error ex, consequatur quia accusantium commodi.</span>
        </div>
        </div>
        
    </div>


</template>

<script>
    export default {
        props:['error'],
        data() {
            return {
                search: null,
                results:false
            }
        },
        methods: {
            appSearch() {
                this.$emit('changeSearch',this.search)
                this.search = null
            }
        }
    }
</script>

<style scoped>

    .searchList{
        display: flex;
        flex-direction: row;
        padding: 2rem;
        background-color: #045fb5;
        margin: 10px;
        color: white;

    }

    .searchList:nth-child(odd){
        background-color:#0379ea4a;
        color: black;
    }

    .input-box {
        display: flex;
        justify-content: space-between;
        margin: 10px;
    }

     

    .input-container {
        background-color: white;
        width: 70%;
        border-radius: 5px;
        margin-bottom: 2rem;
    }

    @media only screen and (max-width: 750px) {
         .input-container{
             width: 100%;
         }
     }

    input {
        font-size: 20px;
        margin-right: 10px;
    }

    .btn {
        width: 7rem;
    }

    .no-result {
        color: red;
        font-size: 26px;
    }
</style>