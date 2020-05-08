<template>
  <div class="container">
    <h1><span>Welcome To</span> Critterpoo Critterpedia!</h1>
    <h2>A Poo Touchers Product</h2>

    <article>
      <h3>What Is This?</h3>
      <p>An unofficail Critterpedia app based off Animal Crossing New Horizons. If you are reading this then odds are your name is either Anna, Nate, or Tina. If its not then please please please don't tell Nintendo. If you work for Nintendo then please don't sue me. This took me too long to make and frankly I don't want to hire a lawyer. Ok go look at the animals. If you see an error please <a href="https://www.youtube.com/watch?v=oHg5SJYRHA0" target="_blank">click here</a></p>
    </article>
  </div>
</template>

<script>
export default {
  head(){
    return{
      title: 'Welcome Lawyers!'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/global.scss';

  h1{
    font-size: 2.5rem;
    margin: 15px auto;
    width: 95%;
    span{
      font-size: 1.3rem;
      display:block;
      width: 160px;
      margin: 10px auto;
      background: $gold;
      color: $brown;
      text-shadow: none;
      padding: 5px 10px;
      border-radius: 20px;
      box-shadow: 0px 2px 5px darken($green,10%);
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;
    }

    @media screen and (min-width: 767px) {
      font-size: 4rem;
    }
  }

  h2{
    font-size: 0.8rem;
    padding: 3px 5px;
    background: orange;
    margin: 0 auto;
    text-align: center;
    width: 160px;
    box-shadow: 0px 2px 5px darken($green,10%);
    background-image: url('~@/assets/play-dots.png');
    background-size: 36px 34.5px;
    border-radius: 20px;
    color: #000;
  }

  article{
    width: 95%;
    max-width: 960px;
    margin: 60px auto;
    text-align: center;
    background: $tan;
    overflow: hidden;
    box-sizing: border-box;
    box-shadow: 0px 2px 5px darken($green,10%);
    background-image: url('~@/assets/play-dots.png');
    background-size: 36px 34.5px;
    border-radius: 20px;
    color: $brown;
    font-family: $headFont;
    font-size: 1.2rem;
    text-shadow: 1px 1px 3px darken($tan,10%);

    p{
      line-height: 2rem;
      padding: 25px;
    }

    a{color: $brown;}

    h3{
      font-family: $headFont;
      font-size: 1.8rem;
      color: $gold;
      background: $brown;
      margin: 0;
      text-shadow: 1px 1px 3px darken($brown,10%);
      padding: 20px;
      background-image: url('~@/assets/play-dots.png');
      background-size: 36px 34.5px;
    }
  }
</style>

