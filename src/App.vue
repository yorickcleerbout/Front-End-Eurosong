<template>
  <div id="app">
    <!-- Home Page -->
    <Homepage v-if="page == 'home'" @change-page="goToPage"/>

    <!-- Game -->
    <Gamepage v-if="page == 'game'" @change-page="goToPage"/>

    <!-- Ranking -->
    <Rankingpage v-if="page == 'ranking'" @change-page="goToPage"/>
    


  </div>
</template>

<script>

// Pages
import Homepage from './components/pages/Home.vue';
import Gamepage from './components/pages/Game.vue';
import Rankingpage from './components/pages/Ranking.vue';

export default {
  name: 'App',
  components: {
    Homepage,
    Gamepage,
    Rankingpage
  },
  data(){
    return {
      page: "home"
    }
  },
  methods: {
    goToPage(page) {
      this.page = page;
    }
  }
  
}
</script>
<style lang="scss">
  @import './scss/style.scss';
</style>