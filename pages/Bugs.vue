<template>
  <div id="bugs">
    <h1>Bugs</h1>

    <Filters :critters="bugList" @filtered="setFilter"/>
    
    <div class="animal-grid">
      <div class="card-contain" v-for="bug of activeList" :key="bug.title">
        <Card :critter="bug" critterType="bugs" />
      </div>
    </div>
  </div>
</template>


<script>
import Card from '@/components/Card.vue';
import Filters from '@/components/Filters';
import bugies from '~/static/bugs.json';
const rightNow = new Date();
const nowHour = rightNow.getHours();
const nowMonth = rightNow.getMonth();
export default {
  name: 'Bugs',
  head(){
    return{
      title: 'Bugs'
    }
  },
  components:{
    Card,
    Filters
  },
  data() {
    return {
      activeList: [],
      nowActiveList: [],
      bugList:[],
      search: '',
      activeNow: true,
      filterActive: true,
      filtersOn: false
    }
  },
  beforeMount() {
    this.addBug();
  },
  methods: {
    async addBug(){
      this.bugList = bugies;
    },
    setFilter(filteredList){
      this.activeList = filteredList;
    },
  },
}
</script>