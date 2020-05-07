<template>
  <div id="fish">
    <h1>Fish</h1>

    <div class="search-contain">
      <button @click="filterActive = !filterActive">Only Active: {{ filterActive ? 'On' : 'Off' }}</button>
      <button @click="holdon">More Filters</button>
      <input type="text" placeholder="Search" v-model="search" class="search-bar">
    </div>
    
    <div class="animal-grid" v-if="!loading">
      <Card v-for="fish of activeList" :key="fish.title" :critter="fish" :critterType="'fish'" />
      <!-- <img :src="`/fish/${fish.img}.png`" alt="" v-for="fish of activeList" :key="fish.title"> -->
      
    </div>
  </div>
</template>


<script>
import Card from '@/components/Card.vue';
import fishies from '~/static/fish.json';
const rightNow = new Date();
const nowHour = rightNow.getHours();
const nowMonth = rightNow.getMonth();
export default {
  name: 'Fish',
  components:{
    Card
  },
  data() {
    return {
      activeList: [],
      nowActiveList: [],
      fishList:[],
      loading: true,
      search: '',
      activeNow: true,
      months: ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sept", "oct", "nov", "dec"],
      filterActive: true,
    }
  },
  async beforeMount() {
    this.addFish();
  },
  methods: {
    async addFish(){
      const self = this;
      await fishies.forEach(fish => {
        if(fish.months.includes(this.months[nowMonth]) && fish.times.includes(nowHour)){
          self.nowActiveList.push(fish);
        }
      })
      this.activeList = this.nowActiveList;
      this.fishList = fishies
      this.loading = false;
      
    },
    holdon(){
      alert('this isnt ready yet')
    }
  },
  watch: {
    search: function() {
      if(this.search.length >= 3){
      var self = this;
      this.activeList = [];
      let templist = self.fishList.filter(function(fish) {
        return fish.title.toLowerCase().indexOf(self.search.toLowerCase()) >= 0;
      });
      templist.forEach(fish => {
        this.activeList.push(fish);
      })
      }else if(this.search.length < 3 && this.activeList.length !== this.nowActiveList.length){
        this.activeList = this.nowActiveList;
      }
    },
    filterActive: function () {
      this.activeList = this.filterActive == true ? this.nowActiveList : this.fishList;
    }
  },
}
</script>
