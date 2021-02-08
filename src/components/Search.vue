<template>
    <div class="input-container">
        <div class="input-box">
            <div>
                <input @keyup.enter="appSearch" type="text" placeholder="enter city or zip" v-model="search">
                <button class="btn" @click="appSearch">Search</button>
                <button class="btn" v-show="results" @click="otherResults" :disabled="lockOtherResult">Other Results</button>
                <button class="btn" v-show="hiddenButton" @click="hidden = !hidden">{{hidden ? 'Show List' : 'Hide List'}}</button>
            </div>

            <span v-if="error" class="no-result">No Result</span>


        </div>

    <Loading v-if="isLoading"/>
        <div v-show="!hidden" v-if="results && !isLoading">

            
            <div  @click="resultSearch(result.url)" class="searchList" v-for="(result,index) in searchResults" :key="result + index">
                <span>Name: {{result.name.split(',').slice(0,1).toString()}}</span>
                <br>
                <span>Region: {{result.region}}</span>
                <br>
                <span>Country: {{result.country}}</span>

            </div>




        </div>

    </div>


</template>

<script>
    import axios from 'axios'
    import Loading from './Loading.vue'

    export default {
        props: ['error'],
        components:{
            Loading
        },
        data() {
            return {
                search: "",
                results: false,
                searchResults: [],
                hidden:true,
                isLoading:false,
                hiddenButton:false,
                lockOtherResult:true

            }
        },
        methods: {
            appSearch() {
                if(this.search !== ""){
                this.$emit('changeSearch', this.search)
                this.results = true
                this.hidden = true
                this.hiddenButton = false
                this.lockOtherResult = false
                }
                
                
            },
            resultSearch(result){
                this.lockOtherResult = false
                this.search = result
                this.appSearch()
                this.search = ""
                this.hidden = true
                this.results = false
            },
            otherResults() {
                if(this.search !== "" && !this.lockOtherResult){
                this.lockOtherResult = true
                this.hidden = false
                this.hiddenButton = true
                this.isLoading = true
                const options = {
                    method: 'GET',
                    url: `http://api.weatherapi.com/v1/search.json?key=1590231e5d674493844164905201310&q=${this.search}`,
                }

                axios.request(options).then((response) => {
                    this.searchResults = response.data

                    this.isLoading = false
                })
                }
                

                
            }
        }
    }
</script>

<style scoped>
    .searchList {
    display: flex;
    flex-direction: column;
    padding: 2rem;
    background-color: #e4e4e4;
    margin: 10px;
    color: black;
    border-radius: 6px;
    font-size: 26px;
}

    

    

    .searchList:nth-child(odd) {
        
    background-color: #e4e4e44d;
        color: black;
    }

.searchList:hover{
        background-color: #676565;
        color: white;
        cursor: pointer;
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



    input {
        font-size: 20px;
        margin-right: 10px;
    }

    .btn {
        width: 7rem;
        margin-right: 1rem;
    }

    .no-result {
        color: red;
        font-size: 26px;
    }

    @media only screen and (max-width: 750px) {
        .input-container {
            width: 100%;
        }
    }

    @media only screen and (max-width: 500px) {
        .input-box {
            justify-content: center
        }

        input {
            width: 98%;
            margin-right: 0;
            font-size: 20px;
        }

        .btn {
            width: 100%;
            margin-top: 10px;
        }
    }
</style>