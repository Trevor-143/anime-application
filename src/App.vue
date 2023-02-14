<template>
  <header>
    <div class="top">
      <img src="./assets/bleach.jpg" alt="cover image">
      <div class="inside">
        <h2>Lets Go</h2>
        <p>Here, you'll find everything you need to 
          know about your favorite anime shows and characters.
           So why wait? Start exploring the world of anime with us today!</p>
        <form>
          <input id="search_text" type="text" placeholder="search and...">
          <button id="search_button">Find</button>
        </form>
      </div>
    </div>
  </header>
  <router-view/>
</template>

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
  margin-top: 10px;
  position: relative;
}
#app {
  background: #000000;
}
.top {
  position: relative;
  max-width: 1200px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 380px;
  border-radius: 20px;
  overflow: hidden;
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
  padding-top: 10%;
  
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
  border-radius: 10px;
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
  border-radius: 10px;
  border: 2px solid #000000;
  cursor: pointer;
}
form button:hover {
  color: #000000;
  background: #fff;
}
</style>
