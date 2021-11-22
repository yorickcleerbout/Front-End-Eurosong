<template>
  <div id="app">
    <!-- Nav -->
    <Navigation />

    <!-- Content -->
    <h1>Eurosong Festival</h1>

    <Feedback 
    v-for="(message, index) in messages" 
    :key="index"
    :message="message.message"
    :classType="message.classType" />
    
    <button @click="addMessage">Add Message</button>

  </div>
</template>

<script>
// // Styling
// import style from './scss/style.scss';

// Components
import Navigation from './components/Navigation.vue';
import Feedback from './components/Feedback.vue';

export default {
  name: 'App',
  components: {
    Navigation,
    Feedback
  },
  data(){
    return {
      messages: [
        {
          message: "Er is een fout",
          classType: "warning"
        },
        {
          message: "'T is kapot",
          classType: "error"
        },
        {
          message: "Het werkt",
          classType: "success"
        }
      ]
    }
  },
  methods: {
    addMessage() {
      this.messages.push(
        {
          message: "Nieuw Feedback Item",
          classType: "success"
        }
      )
    }
  }
  
}
</script>
<style lang="scss">
  @import './scss/style.scss';
</style>