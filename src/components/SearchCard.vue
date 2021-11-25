<template>
    <div class="container">
        <div class="search">
            <input type="text" placeholder="Write a word" v-model="inputSearch" >
        </div>
        <div class="cardResult">
            <div class="word">
                {{dict.word}}
            </div>
            <div class="def">
                {{dict.defFirst}} <br>
                

            </div>
            <button @click='getName()' class="btn">Learn more</button>
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
                gotData: [],
                url: 'https://api.dictionaryapi.dev/api/v2/entries/en/',
                dict: {
                    defFirst: 'Первый текст',
                    exampleDef: 'Пример',
                    defSecond: 'Второй пример',
                    defThird: 'Третий пример',
                    defFourth: 'Четвертый пример',
                }


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
            // async getData() {
            //         fetch(`${this.url}${this.inputSearch}`)
            //             .then(res => res.json())
            //             .then(data => this.gotData = data)
            // },
            async getName(){
                const res = await fetch('https://mashape-community-urban-dictionary.p.rapidapi.com/define?term=' + this.inputSearch, {
                    "headers": {
                        "x-rapidapi-host": "mashape-community-urban-dictionary.p.rapidapi.com",
                        "x-rapidapi-key": "e386ac985amsh5bcce1772131ac4p140bc7jsn4d2975289e9e"
                    }
                });
                const data = await res.json();
                this.dict.defFirst = data.list[1].definition
                this.dict.example = data.list[1].example
                this.dict.word = data.list[1].word
                this.dict.defFirst = data.list[6].definition
                this.dict.defThird = data.list[5].definition
                this.dict.defFourth = data.list[4].definition

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