<template>
    <div class="input-container">
        <div class="input-box">
            <div>
                <input type="text" placeholder="enter zip code" v-model="search">
                <button class="btn" @click="appSearch">Search</button>
            </div>

            <span v-if="error" class="no-result">No Result</span>
        </div>

    </div>


</template>

<script>
    export default {
        data() {
            return {
                search: null,
                error:false
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
    .input-box {
        background-color: white;
        padding: 1.5rem;
        border-radius: 5px;
        margin-bottom: 2rem;
        display: flex;
        justify-content: space-between;
    }

    .input-container {
        width: 70%;
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