<template>
  <div class="home">
    
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";

export default {
  name: 'HomeView',
  setup() {
    const shows = ref([])

    onBeforeMount (() => {
      fetch(`https://api.jikan.moe/v4/anime/genre/14/Horror`)
      .then(response => response.json())
      .then(data => {
        shows.value = data
        console.log(shows.value)
      })
    })    
  }
  
}
</script>
