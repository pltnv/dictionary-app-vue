<template>
    <div>
        <SearchCard/>
    </div>
</template>


<script>
    import SearchCard from "../components/SearchCard";
    export default {
        name: 'Home',
        components: {
            SearchCard
        },
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
                    synonyms: {},
                },
                visibleMore: 'False',
                audioSrc: '',
            }
        },
        methods: {
            async getName() {
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
            }
        }
    }
</script>



