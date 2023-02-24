<template>
  <main>
    <h1>Detail {{ $route.params.mal_id }}</h1>
  </main>
</template>

<script>

import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";

export default {
    setup() {
        const anime = ref({});
        const route = useRoute();

        onBeforeMount(() => {
          fetch(`https://api.jikan.moe/v4/anime/${ route.params.mal_id }/full`)
          .then(response => response.json())
          .then(data => {
              anime.value = data.data;
              console.log(anime.value)
          })
          fetch(`https://api.jikan.moe/v4/characters/${ route.params.mal_id }/voices`)
          .then(response => response.json())
          .then(chara => {
            console.log(chara.data)
          })
        })
        return {
            anime
        }
    }
}
</script>

<style scoped>
  h1 {
    color: #fff;
  }
</style>