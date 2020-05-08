<template>
  <div id="bugs">
    <h1>Bugs</h1>

    <div class="search-contain">
      <button @click="filterActive = !filterActive">Only Active: {{ filterActive ? 'On' : 'Off' }}</button>
      <button @click="newThisMonth" v-if="!filtersOn">New This Month</button>
      <button @click="filtersOn = false; activeList = nowActiveList;" v-if="filtersOn">Clear Filter</button>
      <input type="text" placeholder="Search" v-model="search" class="search-bar">
    </div>
    
    <div class="animal-grid" v-if="!loading">
      <div class="card-contain" v-for="bug of activeList" :key="bug.title">
        <Card :critter="bug" critterType="bugs" />
      </div>
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
  head(){
    return{
      title: 'Bugs'
    }
  },
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
      months: ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sept", "oct", "nov", "dec"],
      filterActive: true,
      filtersOn: false
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
          self.nowActiveList.push(bug);
        }
      })
      this.activeList = this.nowActiveList;
      this.bugList = Object.freeze(bugies)
      this.loading = false;
      
    },
    holdon(){
      alert('this isnt ready yet')
    },
    newThisMonth(){
      this.filtersOn = true;
      const lastMonth = nowMonth - 1 >= 0 ? nowMonth - 1 : 12;
      this.activeList = [];
      const self = this;
      this.bugList.forEach(item => {
        if(!item.months.includes(self.months[lastMonth]) && item.months.includes(self.months[nowMonth])){
          self.activeList.push(item)
        }
      })
    }
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
        this.activeList.push(bug);
      })
      }else if(this.search.length < 3 && this.activeList.length !== this.nowActiveList.length){
        this.activeList = this.nowActiveList;
      }
    },
    filterActive: function () {
      this.filtersOn = false;
      this.activeList = this.filterActive == true ? this.nowActiveList : this.bugList;
    }
  },
}
</script>


