<template>
    <div class="input-container">
        <div class="input-box">
            <div>
                <input type="text" placeholder="enter city or zip" v-model="search">
                <button class="btn" @click="appSearch">Search</button>
            </div>

            <span v-if="error" class="no-result">No Result</span>

           
        </div>
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


</template>

<script>
    export default {
        props:['error'],
        data() {
            return {
                search: null,
            }
        },
        methods: {
            appSearch() {
                this.$emit('changeSearch',this.search)
            }
        }
    }
</script>

<style scoped>
    .searchList{
        display: flex;
        flex-direction: row;
        padding: 2rem;
    }

    .searchList:nth-child(odd){
        background-color:#80808030;
    }

    .input-box {
        display: flex;
        justify-content: space-between;
    }

    .input-container {
        background-color: white;
        width: 65%;
        padding: 1.5rem;
        border-radius: 5px;
        margin-bottom: 2rem;
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