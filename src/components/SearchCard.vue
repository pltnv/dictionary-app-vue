<template>
    <div class="container">
        <div class="search">
            <input type="text" placeholder="Write a word" v-model="inputSearch" >
            <button class="btn"  @click='getName()'>Search</button>
        </div>
        <div v-if="dict" class="cardResult" >
            <div class="word">
                {{ dict.word }} : {{ dict.phonetics }}
            </div>
            <div class="def">
                {{dict.defFirst}} <br>
            </div>
            <button class="btn" @click="visibleMore = !visibleMore">Learn more</button>
            <div class="more" v-if="!visibleMore">
                <div>
                    <span class="phonetic">Phonetic</span> {{ dict.phonetics }}
                </div>
                <div>
                    <span class="origin">Origin</span>  {{ dict.origin }}
                </div>
                <br>
                <div>
                    <span>{{ dict.word }}</span>
                    <div> Definition: {{ dict.defSecond }}</div>
                    <div><span> Synonyms:</span> {{ dict.synonyms }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                inputSearch: '',
                gotData: [],
                url: 'https://api.dictionaryapi.dev/api/v2/entries/en/',
                dict: {
                    defFirst: 'Первый текст',
                    exampleDef: 'Пример',
                    defSecond: 'Второй пример',
                    phonetics: '',
                    origin: '',
                    synonyms: {

                    },
                },
                visibleMore: 'False',
                audioSrc: '',



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
            // sendDataByRoute() {
            //     this.$router.push({name: 'MoreInfo', params:{data: this.dict.synonyms}})
            // },
            // async getData() {
            //         fetch(`${this.url}${this.inputSearch}`)
            //             .then(res => res.json())
            //             .then(data => this.gotData = data)
            // },
            // async getName(){
            //     const res = await fetch('https://mashape-community-urban-dictionary.p.rapidapi.com/define?term=' + this.inputSearch, {
            //         "headers": {
            //             "x-rapidapi-host": "mashape-community-urban-dictionary.p.rapidapi.com",
            //             "x-rapidapi-key": "e386ac985amsh5bcce1772131ac4p140bc7jsn4d2975289e9e"
            //         }
            //     });
            //     const data = await res.json();
            //     this.dict.defFirst = data.list[1].definition
            //     this.dict.example = data.list[1].example
            //     this.dict.word = data.list[1].word
            //     this.dict.defFirst = data.list[6].definition
            //     this.dict.defThird = data.list[5].definition
            //     this.dict.defFourth = data.list[4].definition
            //
            // },
            async getName(){

                const res = await fetch('https://api.dictionaryapi.dev/api/v2/entries/en/' + this.inputSearch);
                const data = await res.json();
                this.dict.defFirst = data[0].meanings[0].definitions[0].definition
                this.dict.word = data[0].word
                this.dict.phonetics = data[0].phonetics[0].text
                this.dict.origin = data[0].origin
                this.audioSrc = 'https://' + data[0].phonetics[0].audio.slice(6)
                this.dict.defSecond = data[0].meanings[0].definitions[1].definition
                this.dict.synonyms = data[0].meanings[0].definitions[0].synonyms.join(', ')





                this.inputSearch = ''
                // this.dict.defFirst = data.list[1].definition
                // this.dict.example = data.list[1].example
                // this.dict.word = data.list[1].word
                // this.dict.defFirst = data.list[6].definition
                // this.dict.defThird = data.list[5].definition
                // this.dict.defFourth = data.list[4].definition

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