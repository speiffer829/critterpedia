<template>
  <div id="bug">
    <h1>Bug</h1>

    <div class="search-contain">
      <input type="text" placeholder="Search" v-model="search" class="search-bar">
    </div>
    
    <div class="animal-grid" v-if="!loading">
      <Card v-for="bug of bugList" :key="bug.title" :critter="bug" v-show="activeList.includes(bug.title)" critterType="bugs" />
      <!-- <img :src="`/bug/${bug.img}.png`" alt="" v-for="bug of activeList" :key="bug.title"> -->
      
    </div>
  </div>
</template>


<script>
import Card from '@/components/Card.vue';
import bugies from '~/static/bugs.json';
const rightNow = new Date();
const nowHour = rightNow.getHours();
const nowMonth = rightNow.getMonth();
export default {
  name: 'Bugs',
  components:{
    Card
  },
  data() {
    return {
      activeList: [],
      nowActiveList: [],
      bugList:[],
      loading: true,
      search: '',
      activeNow: true,
      months: ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sept", "oct", "nov", "dec"]
    }
  },
  async beforeMount() {
    this.addBug();
  },
  methods: {
    async addBug(){
      const self = this;
      await bugies.forEach(bug => {
        if(bug.months.includes(this.months[nowMonth]) && bug.times.includes(nowHour)){
          self.nowActiveList.push(bug.title);
        }
      })
      this.activeList = this.nowActiveList;
      this.bugList = Object.freeze(bugies)
      this.loading = false;
      
    },
  },
  watch: {
    search: function() {
      if(this.search.length >= 3){
      var self = this;
      this.activeList = [];
      let templist = self.bugList.filter(function(bug) {
        return bug.title.toLowerCase().indexOf(self.search.toLowerCase()) >= 0;
      });
      templist.forEach(bug => {
        this.activeList.push(bug.title);
      })
      }else if(this.search.length < 3 && this.activeList.length !== this.nowActiveList.length){
        this.activeList = this.nowActiveList;
      }
    }
  },
}
</script>

<style lang="scss">
@import '@/assets/global.scss';


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
</style>
