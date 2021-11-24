<template>
    <div>
        <SearchCard/>
    </div>

</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import SearchCard from "../components/SearchCard";

export default {
  name: 'Home',
  components: {
    HelloWorld, SearchCard
  }
}
</script>
