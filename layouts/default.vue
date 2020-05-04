<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link to="/Fish">Fish</router-link>
      <router-link to="/Bugs">Bugs</router-link>
    </div>
    <nuxt />
  </div>
</template>

<style lang="scss">
@import '@/assets/global.scss';

body{
  background-color: $green;
  background-image: url('~@/assets/green-triangles.png');
  background-size: 156px 154.5px;
  margin: 0;
}

#app {
  font-family: $font;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1{
  text-align: center;
  font-size: 4rem;
  color: $gold;
  font-family: $headFont;
  text-shadow: 2px 2px 5px darken($green, 15%);
}

#nav {
  padding: 30px;
  display: grid;
  justify-content: center;
  max-width: 330px;
  grid-template-columns: 1fr 1fr 1fr;
  justify-content: center;
  margin: 0 auto;
  grid-gap: 0.8rem;


  a {
    font-weight: bold;
    background-color: $brown;
    color: $gold;
    text-shadow: 1px 1px 3px darken($brown, 10%);
    background-image: url('~@/assets/play-dots.png');
    background-size: 36px 34.5px;
    padding: 0.4rem;
    text-decoration: none;
    font-family: $headFont;
    border-radius: 0.2rem;
    font-size: 1.3rem;
    text-align: center;
    box-shadow: 0px 2px 5px darken($green, 15%);
    transition: all 250ms;

    &:hover{
      transform: scale(1.15);
    }

    &.nuxt-link-exact-active {
      background-color: $gold;
      color: $brown;
      text-shadow: 1px 1px 3px darken($gold, 15%);
      transform: scale(0.85)
    }
  }
}

.animal-grid{
  display: grid;
  grid-gap: 2rem;
  margin: 10px auto;
  max-width: 1200px;
  width: 95%;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  justify-content: center;
  padding-bottom: 2rem;
}


.search-contain{
  max-width: 960px;
  width: 95%;
  margin: 20px auto;

  input{
    width: 100%;
    font-size: 2rem;
    padding: 0.6rem;
    font-family: $headFont;
    background: $tan;
    color: $brown;
    border: solid 3px $brown;
    border-radius: 10px;
    box-sizing: border-box;
    display: block;
  }
}
</style>
