<template>
  <div class="filters">
    <div class="search-contain">
        <button @click="filterActive = !filterActive">Only Active: {{ filterActive ? 'On' : 'Off' }}</button>
        <button @click="newThisMonth" v-if="!filtersOn">New This Month</button>
        <button @click="filtersOn = false; activeList = nowActiveList;" v-if="filtersOn">Clear Filter</button>
        <input type="text" placeholder="Search" v-model="search" class="search-bar" />
    </div>
  </div>
</template>


<script>
const rightNow = new Date();
const nowHour = rightNow.getHours();
const nowMonth = rightNow.getMonth();
export default {
  name: 'Filters',
  props: {
    critters: Array
  },
  data() {
    return {
      months: ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sept", "oct", "nov", "dec"],
      filterActive: true,
      filtersOn: false,
      search: '',
      activeList: [],
      nowActiveList: [],
    }
  },
  mounted() {
    const self = this;
      this.critters.forEach(critter => {
        if(critter.months.includes(this.months[nowMonth]) && critter.times.includes(nowHour)){
         self.nowActiveList.push(critter);
        }
      })

      this.activeList = this.nowActiveList;
  },
  methods: {
    newThisMonth(){
      this.filtersOn = true;
      const lastMonth = nowMonth - 1 >= 0 ? nowMonth - 1 : 12;
      this.activeList = [];
      const self = this;
      this.critters.forEach(item => {
        if(!item.months.includes(self.months[lastMonth]) && item.months.includes(self.months[nowMonth])){
          self.activeList.push(item)
        }
      })
    }
  },
  watch: {
    activeList: function() {
      this.$emit('filtered', this.activeList);
    },
    search: function() {
      if(this.search.length >= 3){
      var self = this;
      this.activeList = [];
      let templist = self.critters.filter(function(critter) {
        return critter.title.toLowerCase().indexOf(self.search.toLowerCase()) >= 0;
      });
      templist.forEach(critter => {
        this.activeList.push(critter);
      })
      }else if(this.search.length < 3 && this.activeList.length !== this.nowActiveList.length){
        this.activeList = this.nowActiveList;
      }
    },
    filterActive: function () {
      this.filtersOn = false;
      const activeList = this.filterActive == true ? this.nowActiveList : this.critters;
      this.$emit('filtered', activeList);
    }
  },
}
</script>


<style>
  
</style>