<template>
  <div id="app">
    <!-- Nav -->
    <nav class="c-nav">
      <ul class="c-nav-list">
        <li class="c-nav-list-item">Home</li>
        <li class="c-nav-list-item">Contact</li>
      </ul>
    </nav>

    <!-- Content -->
    <h1>Eurosong Festival</h1>

    <div class="c-feedback warning">Er is een fout gebeurd</div>
    <div class="c-feedback error">'T is kapot</div>
    <div class="c-feedback success">Het werkt</div>
    
  </div>
</template>

<script>
// Import styling for the whole app
import style from './scss/style.scss';

export default {
  name: 'App',
  
}
</script>

