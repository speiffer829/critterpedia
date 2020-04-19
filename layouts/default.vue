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

    &.router-link-exact-active {
      background-color: $gold;
      color: $brown;
      text-shadow: 1px 1px 3px darken($gold, 15%);
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

  .card{
    background-color: $tan;
    background-image: url('~@/assets/play-dots.png');
    background-size: 36px 34.5px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-areas: 
      'pic pic pic'
      'title title title'
      'price price price'
      'size location location'
      'month time time';
    border-radius: 0.5rem;
    filter: drop-shadow(2px 2px 10px darken($green,10%));
    margin-top: 40px;
    text-align: center;

    .img-bar{
      height: 10px;
      border-radius: 0.5rem 0.5rem 0 0;
      grid-area: pic;
      position: relative;
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;

      .img-align{
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        top: -40px;

        .img-circle{
          width: 80px;
          height: 80px;
          display: flex;
          justify-content: center;
          align-items: center;
          border-radius: 200px;
          background-image: url('~@/assets/play-dots.png');
          background-size: 36px 34.5px;

          img{
            display: block;
          }
        }
      }
    }

    .title{
      font-size: 2rem;
      color: $gold;
      font-family: $headFont;
      padding: 0.8rem;
      padding-top: 2.2rem;
      font-weight: bold;
      background: $brown;
      margin: 0;
      text-shadow: 2px 2px 5px darken($brown, 10%);
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;
      grid-area: title;
    }

    .head{
      margin: 0 auto;
      text-align: center;
      font-family: $headFont;
      font-weight: bold;
      display: inline-block;
      background: $gold;
      color: darken($brown, 5%);
      padding: 5px 10px;
      text-align: center;
      border-radius: 20px;
      margin-top: 10px;
      // text-shadow: 1px 1px 0px darken($brown, 5%);
    }

    .stat{
      font-size: 1.2rem;
      text-transform: capitalize;
      font-weight: bold;
      font-family: $headFont;
      margin: 10px 0;
    }

    .months{
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 5px;
      padding: 10px;
      color: $brown;
      grid-area: month;

      span{
        border-radius: 4px;
        text-align: center;
        color: $brown;
        font-weight: bold;
        border: solid 2px $brown;
        display: block;
        box-sizing: border-box;
        background: $tan;

        &.active{
          background: $brown;
          color: $gold;
        }
      }
    }

    .times{
      grid-area: time;
      // background: radial-gradient(lighten($blue, 15%), $blue);
      color: $brown;
      padding: 10px;
      
      .time-grid{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 5px;

        .head{
          grid-column: span 2;
        }
      }

      span{
        border-radius: 4px;
        text-align: center;
        color: $brown;
        font-weight: bold;
        border: solid 2px $gold;
        width: 100%;
        display: block;
        box-sizing: border-box;
        background: $tan;

        &.active{
          background-color: $gold;
          color: #000;
        }
      }
      
      p{
        text-align: center;
        font-family: $headFont;
      }
    }

    .location{
      grid-area: location;
      padding: 10px;
      color: $gold;
      background-color: darken($brown,15%);
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;s
      
      p{
        text-align: center;
        font-family: $headFont;
      }
    }

    .size{
      grid-area: size;
      padding: 10px;
      color: $gold;
      background-color: darken($brown,10%);
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;
      
      p{
        text-align: center;
        font-family: $headFont;
      }
    }

    .price{
      grid-area: price;
      padding: 10px;
      color: $brown;
      background-color: $gold;
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;

      .head{
        background: none;
        color: $tan;
        text-shadow: 1px 1px 0px darken($tan, 70%);
      }

      .stat{
        font-size: 2rem;
        color: $tan;
        text-shadow: 1px 1px 0px darken($tan, 70%);
      }
      
      p{
        text-align: center;
        font-family: $headFont;
      }
    }
  }
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
