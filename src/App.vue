<template>
  <div id="app">
    <!-- Home Page -->
    <div v-if="page == 'home'">
        <h1>
          Eurosong Voting App
        </h1>

        <button @click="goToGame">Show Game</button>
        <button @click="goToRanking">Show Ranking</button>
    </div>
    

    <!-- Game -->
    <div v-if="page == 'game'">
      <h1>Game</h1>
    </div>

    <!-- Ranking -->
    <div v-if="page == 'ranking'">
      <h1>Ranking</h1>
    </div>


  </div>
</template>

<script>

// Components
//import Feedback from './components/Feedback.vue';

export default {
  name: 'App',
  components: {
  
  },
  data(){
    return {
      page: "home"
    }
  },
  methods: {
    goToGame() {
      this.page = "game";
    },

    goToRanking() {
      this.page = "ranking";
    }
  }
  
}
</script>
<style lang="scss">
  @import './scss/style.scss';
</style>