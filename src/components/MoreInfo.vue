<template>
    <div class="container">
        <div class="cardInfo">
            <span> {{word}} </span>
            <hr>
            <div>
                <div> {{ defSecond }}</div>
                <div>{{ synonyms }}</div>
            </div>

        </div>
    </div>
</template>

<script>
    export default {
      name: "MoreInfo.vue",
      props: ['word'],
      data() {
        return {}
      }
    }
</script>

<style scoped>

</style>