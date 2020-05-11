<template>
  <div id="bugs">
    <h1>Bugs</h1>

    <Filters :critters="bugList" @filtered="setFilter"/>
    
    <div class="animal-grid" v-if="!loading">
      <div class="card-contain" v-for="bug of activeList" :key="bug.title">
        <Card :critter="bug" critterType="bugs" />
      </div>
    </div>
  </div>
</template>


<script>
import Card from '@/components/Card.vue';
import Filters from '@/components/Filters'
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
      loading: true,
      search: '',
      activeNow: true,
      months: ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sept", "oct", "nov", "dec"],
      filterActive: true,
      filtersOn: false
    }
  },
  async beforeMount() {
    this.addBug();
  },
  methods: {
    addBug(){
      this.bugList = bugies;
      this.loading = false;
    },
    setFilter(filteredList){
      this.activeList = filteredList;
    },
  },
}
</script>


