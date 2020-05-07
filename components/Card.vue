<template>
  <div class="card" @click="expanded = !expanded">
    <div class="img-bar" :style="{backgroundColor: imgColor}">
      <div class="img-align">
        <div class="img-circle" :style="{backgroundColor: imgColor}">
          <img :src="imgGet" :alt="critter.title" lazy>
          <span class="active-dot" :style="{backgroundColor: isActive}"></span>
        </div>
      </div>
    </div>
    <p class="title">{{ critter.title }}</p>
    
    <div class="months" :class="{'expanded' : expanded}">
      <div class="months-grid">
        <p class="head">Months</p>
        <span :class="{ 'active' : critter.months.includes('jan') }">Jan</span>
        <span :class="{ 'active' : critter.months.includes('feb') }">Feb</span>
        <span :class="{ 'active' : critter.months.includes('mar') }">Mar</span>
        <span :class="{ 'active' : critter.months.includes('apr') }">Apr</span>
        <span :class="{ 'active' : critter.months.includes('may') }">May</span>
        <span :class="{ 'active' : critter.months.includes('jun') }">Jun</span>
        <span :class="{ 'active' : critter.months.includes('jul') }">Jul</span>
        <span :class="{ 'active' : critter.months.includes('aug') }">Aug</span>
        <span :class="{ 'active' : critter.months.includes('sept') }">Sept</span>
        <span :class="{ 'active' : critter.months.includes('oct') }">Oct</span>
        <span :class="{ 'active' : critter.months.includes('nov') }">Nov</span>
        <span :class="{ 'active' : critter.months.includes('dec') }">Dec</span>
      </div>
    </div>

    <div class="times" :class="{'expanded' : expanded}">
      <div class="time-grid">
        <p class="head">Time Active</p>
        <span :class="{ 'active' : critter.times.includes(1) }">1 am</span>
        <span :class="{ 'active' : critter.times.includes(13) }">1 pm</span>
        <span :class="{ 'active' : critter.times.includes(2) }">2 am</span>
        <span :class="{ 'active' : critter.times.includes(14) }">2 pm</span>
        <span :class="{ 'active' : critter.times.includes(3) }">3 am</span>
        <span :class="{ 'active' : critter.times.includes(15) }">3 pm</span>
        <span :class="{ 'active' : critter.times.includes(4) }">4 am</span>
        <span :class="{ 'active' : critter.times.includes(16) }">4 pm</span>
        <span :class="{ 'active' : critter.times.includes(5) }">5 am</span>
        <span :class="{ 'active' : critter.times.includes(17) }">5 pm</span>
        <span :class="{ 'active' : critter.times.includes(6) }">6 am</span>
        <span :class="{ 'active' : critter.times.includes(18) }">6 pm</span>
        <span :class="{ 'active' : critter.times.includes(7) }">7 am</span>
        <span :class="{ 'active' : critter.times.includes(19) }">7 pm</span>
        <span :class="{ 'active' : critter.times.includes(8) }">8 am</span>
        <span :class="{ 'active' : critter.times.includes(20) }">8 pm</span>
        <span :class="{ 'active' : critter.times.includes(9) }">9 am</span>
        <span :class="{ 'active' : critter.times.includes(21) }">9 pm</span>
        <span :class="{ 'active' : critter.times.includes(10) }">10 am</span>
        <span :class="{ 'active' : critter.times.includes(22) }">10 pm</span>
        <span :class="{ 'active' : critter.times.includes(11) }">11 am</span>
        <span :class="{ 'active' : critter.times.includes(23) }">11 pm</span>
        <span :class="{ 'active' : critter.times.includes(12) }">12 pm</span>
        <span :class="{ 'active' : critter.times.includes(0) }">12 am</span>
      </div>
    </div>

    <div class="location" :class="{'expanded' : expanded}">
      <p class="head">Location</p>
      <p class="stat">{{ critter.location }}</p>
    </div>

    <div class="size" :class="{'expanded' : expanded}">
      <p class="head">Size</p>
      <p class="stat">{{ critter.size }}</p>
    </div>

    <div class="price" :style="{backgroundColor: imgColor}">
      <!-- <p class="head">Price</p> -->
      <p class="stat">${{ prettNum }}</p>
    </div>
  </div>
</template>


<script>
export default {
  name: 'Card',
  props:{
    critter: {
      type: Object,
      required: true,
      default: {
        title: 'Critter',
        price: 0,
        location: 'unknown',
        months: [],
        times: [],
      }
    },
    critterType: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      expanded: false
    }
  },
  computed: {
    imgGet(){
      return require(`../assets/${this.critterType}/${this.critter.img}.png`);
      // return `@/${this.critterType}/${this.critter.img}.png`
    },
    imgColor(){
      const price = this.critter.price;
      if(price >= 10000){
        return '#FCCC1F';
      }else if(price >= 5000){
        return '#B6A2C8';
      }else if(price >= 1000){
        return '#74A1D2';
      }else{
        return '#D1DB63';
      }
    },
    prettNum(){
      const num = this.critter.price
      var num_parts = num.toString().split(".");
      num_parts[0] = num_parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      return num_parts.join(".");
    },
    isActive(){
      const rightNow = new Date();
      const nowHour = rightNow.getHours();
      const nowMonth = rightNow.getMonth();
      const months = ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sept", "oct", "nov", "dec"];

      if(this.critter.months.includes(months[nowMonth]) && this.critter.times.includes(nowHour)){
        return '#00A144';
      }else{
        return '#5c5c5c';
      }
    }
  },
}
</script>

<style lang="scss">
  .card{
    cursor: pointer;
  }
  .img-circle{
    position: relative;
  }
  .active-dot{
    width: 12px;
    height: 12px;
    background: #5c5c5c;
    border: solid 2px #fff;
    border-radius: 100px;
    position: absolute;
    right: 8px;
    bottom: 0;
  }

  .months,.times{
    transition: height 250ms;
    overflow: hidden;
    height: 0;

    &.expanded{
      height: 467px;
    }
  }

  .location, .size{
    transition: height 250ms;
    overflow: hidden;
    height: 0;

    &.expanded {
      height: 83px;
    }
  }
</style>
