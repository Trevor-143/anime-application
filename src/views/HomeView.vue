<template>
  <main>
    <div class="topAnime">
      <h2>Top Anime</h2>
      <ul class="topAnimeSingles">
        <li v-for="anime in shows" :key="anime.mal_id">
          <img :src="anime.images.webp.image_url" :alt="anime.title">
          <div class="info">
            <h3>{{ anime.title }}</h3>
            <h4>{{ anime.score }}</h4>
          </div>
        </li>
      </ul>
    </div>
    <div class="topAnime">
      <h2>Upcoming Anime Seasons</h2>
      <ul class="topAnimeSingles">
        <li v-for="anime in seasons" :key="anime.mal_id">
          <img :src="anime.images.webp.image_url" :alt="anime.title">
          <div class="info">
            <h3>{{ anime.title }}</h3>
            <h4>{{ anime.score }}</h4>
          </div>
        </li>
      </ul>
    </div>
  </main>
</template>

<script>
import { ref, onBeforeMount } from "vue";

export default {
  name: 'HomeView',
  setup() {
    const shows = ref([])
    const randoms = ref([])
    const seasons = ref([])

    onBeforeMount(() => {
      fetch(`https://api.jikan.moe/v4/top/anime`)
      .then(response => response.json())
      .then(data => {
        shows.value = data.data
        // console.log(shows.value)
      })
      fetch(`https://api.jikan.moe/v4/seasons/upcoming`)
      .then(response => response.json())
      .then(data => {
        seasons.value = data.data
        // console.log(seasons.value)
      })
    })

    
    return {
      shows,
      randoms,
      seasons
    }
  }
}

</script>

<style>

.topAnime {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.topAnimeSingles {
  max-width: 1200px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;

}
.topAnime h2 {
  padding: 5px 10px;
  margin-top: 20px;
  color: #333333;
  border-radius: 10px;
  font-size: 25px;
  
}
.topAnimeSingles li {
  padding: 10px;
  margin: 5px;
  list-style-type: none;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

}
.topAnimeSingles li img {
  width: 170px;
  height: 200px;
  object-fit: cover;
  border-radius: 10px;
}
.topAnimeSingles li .info {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
}
.topAnimeSingles h3 {
  max-width: 160px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2; /* number of lines to show */
          line-clamp: 2; 
  -webkit-box-orient: vertical;
  color: #ffffff;
  text-align: center;
}
.topAnimeSingles li h4 {
  color: #fff;
  height: 40px;
  border-radius: 10px;
  margin: 5px 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>