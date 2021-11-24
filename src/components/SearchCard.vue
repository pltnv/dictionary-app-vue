<template>
    <div class="container">
        <div class="search">
            <input type="text" placeholder="Write a word" v-model="inputSearch" >
        </div>
        <div class="cardResult">
            <div class="word">
                {{gotData[0].word}}
            </div>
            <div class="def">
               {{gotData[0].meanings[0].definitions[0].definition}}
            </div>
            <button @click='getData()' class="btn">Learn more</button>
             <br>


        </div>



    </div>
</template>

<script>
    export default {
        data() {
            return {
                kek: '30',
                inputSearch: 'hello',
                gotData: '',
                url: 'https://api.dictionaryapi.dev/api/v2/entries/en/',


            }
        },
        // mounted() {
        //     fetch(this.url)
        //         .then(res => res.json())
        //         .then(data => this.gotData = data)
        //         .catch(err => console.log(err.message))
        // },
        // async mounted() {
        //     const resp = await fetch(this.url)
        //     const res = await resp.json()
        //     this.gotData.push(res);
        // },
        methods: {
            getData() {
                    fetch(`${this.url}${this.inputSearch}`)
                        .then(res => res.json())
                        .then(data => this.gotData = data)
            }
        }



    }
</script>











<style scoped>
    .container{
        background-color: #8e9b94;
        width: 500px;
        max-height: 400px;

    }

    .def{
        font-family: "Apple Chancery";
        font-size: 30px;
    }

    .cardResult{
        background-color: bisque;
    }

    .search{


    }
    .search > input {
        height: 50px;
        width: 400px;
        border-radius: 20px;
        padding: 5px;

    }

    .btn{
        border-radius: 20px;

    }

</style>