<template>
  <div class="card">
    <div class="img-bar" :style="{backgroundColor: imgColor}">
      <div class="img-align">
        <div class="img-circle" :style="{backgroundColor: imgColor}">
          <img :src="`/fish/${fish.img}.png`" alt="fish">
        </div>
      </div>
    </div>
    <p class="title">{{ fish.title }}</p>
    
    <div class="months">
      <p class="head">Months</p>
      <span :class="{'active' : jan}">Jan</span>
      <span :class="{'active' : feb}">Feb</span>
      <span :class="{'active' : mar}">Mar</span>
      <span :class="{'active' : apr}">Apr</span>
      <span :class="{'active' : may}">May</span>
      <span :class="{'active' : jun}">Jun</span>
      <span :class="{'active' : jul}">Jul</span>
      <span :class="{'active' : aug}">Aug</span>
      <span :class="{'active' : sept}">Sept</span>
      <span :class="{'active' : oct}">Oct</span>
      <span :class="{'active' : nov}">Nov</span>
      <span :class="{'active' : dec}">Dec</span>
    </div>

    <div class="times">
      <div class="time-grid">
        <p class="head">Time Active</p>
        <span :class="{ 'active' : fish.times.includes(1) }">1 am</span>
        <span :class="{ 'active' : fish.times.includes(13) }">1 pm</span>
        <span :class="{ 'active' : fish.times.includes(2) }">2 am</span>
        <span :class="{ 'active' : fish.times.includes(14) }">2 pm</span>
        <span :class="{ 'active' : fish.times.includes(3) }">3 am</span>
        <span :class="{ 'active' : fish.times.includes(15) }">3 pm</span>
        <span :class="{ 'active' : fish.times.includes(4) }">4 am</span>
        <span :class="{ 'active' : fish.times.includes(16) }">4 pm</span>
        <span :class="{ 'active' : fish.times.includes(5) }">5 am</span>
        <span :class="{ 'active' : fish.times.includes(17) }">5 pm</span>
        <span :class="{ 'active' : fish.times.includes(6) }">6 am</span>
        <span :class="{ 'active' : fish.times.includes(18) }">6 pm</span>
        <span :class="{ 'active' : fish.times.includes(7) }">7 am</span>
        <span :class="{ 'active' : fish.times.includes(19) }">7 pm</span>
        <span :class="{ 'active' : fish.times.includes(8) }">8 am</span>
        <span :class="{ 'active' : fish.times.includes(20) }">8 pm</span>
        <span :class="{ 'active' : fish.times.includes(9) }">9 am</span>
        <span :class="{ 'active' : fish.times.includes(21) }">9 pm</span>
        <span :class="{ 'active' : fish.times.includes(10) }">10 am</span>
        <span :class="{ 'active' : fish.times.includes(22) }">10 pm</span>
        <span :class="{ 'active' : fish.times.includes(11) }">11 am</span>
        <span :class="{ 'active' : fish.times.includes(23) }">11 pm</span>
        <span :class="{ 'active' : fish.times.includes(12) }">12 pm</span>
        <span :class="{ 'active' : fish.times.includes(0) }">12 am</span>
      </div>
    </div>

    <div class="location">
      <p class="head">Location</p>
      <p class="stat">{{ fish.location }}</p>
    </div>

    <div class="size">
      <p class="head">Size</p>
      <p class="stat">{{ fish.size }}</p>
    </div>

    <div class="price" :style="{backgroundColor: imgColor}">
      <!-- <p class="head">Price</p> -->
      <p class="stat">${{ prettNum(fish.price) }}</p>
    </div>
  </div>
</template>


<script>
export default {
  name: 'Card',
  props:{
    fish: Object
  },
  data() {
    return {
      imgColor: '',
      jan: false,
      feb: false,
      mar: false,
      apr: false,
      may: false,
      jun: false,
      jul: false,
      aug: false,
      sept: false,
      oct: false,
      nov: false,
      dec: false,
      img: `/fish/${this.fish.img}.png`,
      publicPath: process.env.BASE_URL,
    }
  },
  mounted() {
    const price = this.fish.price;
    if(price >= 10000){
      this.imgColor = '#FCCC1F';
    }else if(price >= 5000){
      this.imgColor = '#B6A2C8';
    }else if(price >= 1000){
      this.imgColor = '#74A1D2';
    }else{
      this.imgColor = '#D1DB63';
    }

    this.fish.months.forEach(month => {
      this[month] = true;
    });
  },
  methods: {
    prettNum(num){
      var num_parts = num.toString().split(".");
      num_parts[0] = num_parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      return num_parts.join(".");
    }
  },
}
</script>
