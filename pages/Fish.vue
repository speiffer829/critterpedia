<template>
  <div id="fish">
    <h1>Fish</h1>

    <Filters :critters="fishList" @filtered="setFilter"/>
    
    <div class="animal-grid">
      <div class="card-contain" v-for="fish of activeList" :key="fish.title">
        <Card :critter="fish" :critterType="'fish'" />
      </div>
    </div>
  </div>
</template>


<script>
import Card from '@/components/Card.vue';
import Filters from '@/components/Filters';
import fishies from '~/static/fish.json';
const rightNow = new Date();
const nowHour = rightNow.getHours();
const nowMonth = rightNow.getMonth();
export default {
  name: 'Fish',
  components:{
    Card,
    Filters
  },
  head(){
    return{
      title: 'Fish'
    }
  },
  data() {
    return {
      activeList: [],
      nowActiveList: [],
      fishList:[],
      search: '',
      activeNow: true,
      filterActive: true,
      filtersOn: false
    }
  },
  beforeMount() {
    this.addFish();
  },
  methods: {
    async addFish(){
      this.fishList = fishies
    },
    setFilter(filteredList){
      this.activeList = filteredList;
    },
  },
}
</script>