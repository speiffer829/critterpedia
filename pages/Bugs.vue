<template>
  <div id="bugs">
    <h1>Bugs</h1>

    <div class="search-contain">
      <input type="text" placeholder="Search" v-model="search" class="search-bar">
    </div>
    
    <!-- <div class="animal-grid">
      <Card v-for="fish of activeList" :key="fish.title" :fish="fish" />
    </div> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: ''
    }
  },
}
</script>