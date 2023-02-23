<template>
  <header>
    <div class="top">
      <img src="./assets/reina.jpg" alt="cover image">
      <div class="inside">
        <h2>Lets Go</h2>
        <p>Here, you'll find everything you need to 
          know about your favorite anime shows and characters.
           So why wait? Start exploring the world of anime with us today!</p>
        <form @submit.prevent="getSearch">
          <input id="search_text" type="text" placeholder="search and..." v-model="search_text">
          <button id="search_button">Find</button>
        </form>
      </div>
    </div>
  </header>
  <div class="topAnime">
    <h2 class="head"></h2>
    <ul class="topAnimeSingles">
      <li v-for="anime in found" :key="anime.mal_id">
        <img :src="anime.images.webp.image_url" :alt="anime.title">
        <div class="info">
          <h3>{{ anime.title }}</h3>
          <h4>{{ anime.score }}</h4>
        </div>
      </li>
    </ul>
  </div>
  <router-view/>
  <MainFooter />
</template>


<script>

import MainFooter from './components/MainFooter.vue'
import { ref } from 'vue'

export default {
  components: {
    MainFooter
  },
  setup() {
    const found = ref([])
    const search_text = ref('')

    const getSearch = () => {
      if (search_text.value != '') {
        fetch(`https://api.jikan.moe/v4/anime?q=${search_text.value}`)
        .then(resp => resp.json())
        .then(data => {
          found.value = data.data
          search_text.value = ''
          document.querySelector('.head').innerHTML = 'Search Results';
        })
      }
    }
    return {
      getSearch,
      found,
      
      search_text
    }
  }
}

</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'poppins', sans-serif;
  /* background-color: #e6e6e6; */
}
header {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}
#app {
  background: #000000;
}
.top {
  position: relative;
  max-width: 1400px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 380px;
  border-radius: 10px;
  overflow: hidden;
  margin-top: 10px;
  margin-left: 10px;
  margin-right: 10px;
}
.top img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.inside {
  display: flex;
  flex-direction: column;
  position: absolute;
  
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.7);
  width: 100%;
  height: 100%;
  color: #fff;
}
.inside p {
  max-width: 650px;
  text-align: center;
  padding: 10px 0;
}
form {
  display: flex;
  flex-direction: row;
  align-items: center;
  background: #fff;
  padding: 10px;
  padding-left: 25px;
  border-radius: 99px;
  color: #000000;
  width: 70%;
}
form input {
  background: none;
  border: none;
  width: 100%;
}

form input:focus {
  background: none;
  outline: none;
}

form button {
  transition: 0.5s;
  background: #000000;
  color: #fff;
  padding: 7px 15px;
  border-radius: 99px;
  border: 2px solid #000000;
  cursor: pointer;
}
form button:hover {
  color: #000000;
  background: #fff;
}
</style>
