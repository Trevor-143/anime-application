<template>
  <main>
    <div class="topAnime">
      <h2>Top Anime</h2>
      <ul class="topAnimeSingles">
        <li v-for="anime in shows" :key="anime.mal_id">
          <img :src="anime.images.webp.image_url" :alt="anime.title">
          <h3>{{ anime.title }}</h3>
          <h4>{{ anime.score }}</h4>
          <!-- <button @submit.prevent="goWatch()" > Watch Now </button> -->
          <router-link :to="streamLink"> watch Now </router-link>
        </li>
      </ul>
      
    </div>
    <div class="random">
      <ul class="randomAnime">
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
    const streamLink = ref('')
    const streamID = ref('')

    // onBeforeMount(() => {
    //   fetch(`https://api.jikan.moe/v4/top/anime`)
    //   .then(response => response.json())
    //   .then(data => {
    //     shows.value = data.data
    //     console.log(shows.value)
    //     shows.value.forEach(show => {
    //       // console.log(show.mal_id);
    //       streamID.value = show.mal_id
    //     });
        
    //   })
    // })
    // const goWatch = () => {
    //   fetch(`https://api.jikan.moe/v4/anime/${streamID.value}/streaming`)
    //   .then(response => response.json())
    //   .then(data => {
    //     streamLink.value = data.data[1].url
    //     console.log(streamLink.value)
    //   })
    // }

    onBeforeMount(() => {
      fetch(`https://api.jikan.moe/v4/top/anime`)
        .then(response => response.json())
        .then(data => {
          shows.value = data.data
          console.log(shows.value)
          const malIds = shows.value.map(show => show.mal_id);
          streamID.value = malIds;
        });
    });
    
    const goWatch = () => {
      fetch(`https://api.jikan.moe/v4/anime/${streamID.value}/streaming`)
        .then(response => response.json())
        .then(data => {
          const streamingService = 'Crunchyroll'; // replace with the desired service
          const streamData = data.data.find(service => service.service === streamingService);
          if (streamData) {
            streamLink.value = streamData.url;
            console.log(streamLink.value);
          } else {
            console.log(`Streaming link not found for ${streamingService}`);
          }
        });
    };
    

    return {
      shows,
      randoms,
      goWatch,
      streamID,
      streamLink
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

}
.topAnime h2 {
  padding: 5px 10px;
  margin-top: 10px;
  background-color: #000;
  color: #fff;
  border-radius: 10px;
  width: fit-content;
  font-size: smaller;
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
  border-radius: 20px;
}
.topAnimeSingles h3 {
  max-width: 160px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2; /* number of lines to show */
          line-clamp: 2; 
  -webkit-box-orient: vertical;
}
.topAnimeSingles li h4 {
  top: 10;
  right: 10;
  background: #000;
  color: #fff;
  width: 100%;
  height: 40px;
  z-index: 2;
  border-radius: 10px;
  margin: 5px 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>