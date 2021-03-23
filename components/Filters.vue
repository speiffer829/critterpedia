<template>
  <div class="filters">
    <div class="search-contain">
        <button @click="activeList = critters; filtersOn = true;" v-if="!filtersOn">Show Currently Active</button>
        <button @click="activeThisMonth" v-if="!filtersOn">Active This Month</button>
        <button @click="newThisMonth" v-if="!filtersOn">New This Month</button>
        <button @click="newNextMonth" v-if="!filtersOn">New Next Month</button>
        <button @click="filtersOn = false; activeList = nowActiveList; search=''; currentFilter='Currently Active'" v-if="filtersOn" class="clear-btn">Clear Filter</button>
        <input type="text" placeholder="Search" v-model="search" class="search-bar" />

        <p class="current-filter" v-if="currentFilter">Showing: "{{ currentFilter }}"</p>
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
      currentFilter: 'Currently Active'
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
      this.currentFilter = `New For ${this.months[nowMonth]}`;
      this.activeList = [];
      const self = this;
      this.critters.forEach(item => {
        if(!item.months.includes(self.months[lastMonth]) && item.months.includes(self.months[nowMonth])){
          self.activeList.push(item)
        }
      })
    },
    newNextMonth(){
      this.filtersOn = true;
      const nextMonth = nowMonth + 1 <= 11 ? nowMonth + 1 : 0;
      console.log( nextMonth )
      this.currentFilter = `New In ${this.months[nextMonth]}.`;
      this.activeList = [];
      const self = this;
      this.critters.forEach(item => {
        if(item.months.includes(self.months[nextMonth]) && !item.months.includes(self.months[nowMonth])){
          self.activeList.push(item)
        }
      })
    },
    activeThisMonth(){
      this.filtersOn = true;
      const self = this;
      this.activeList = [];
      this.currentFilter = `Currently Active in ${this.months[nowMonth]}.`;
      this.critters.forEach(critter => {
        if(critter.months.includes(this.months[nowMonth])){
         self.activeList.push(critter);
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
        this.currentFilter = `Search For ${this.search}`;
        this.filtersOn = true;
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
        this.filtersOn = false;
        this.currentFilter = 'Currently Active';
      }
    },
  },
}
</script>


<style lang="scss">
@import '@/assets/global.scss';
  .clear-btn{
    grid-column: span 2;
  }
  
  .current-filter{
    text-align: center;
    font-size: 1.5rem;
    color: $gold !important;
    grid-column: span 2;
    font-family: $headFont;
    font-weight: bold;
    text-transform: capitalize;
    margin: 10px 0;
  }
</style>