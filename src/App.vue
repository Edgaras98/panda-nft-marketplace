<template>
  <div id="app">
    <Navigation/>
    <router-view/>
  </div>
</template>

<script>
import Navigation from '@/components/Navigation.vue';

export default {
  name: 'app',
  components: {
    Navigation,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700;800&display=swap');
@import 'scss/navigation.scss';
@import 'scss/buttons.scss';

#app {
  font-family: 'Poppins', sans-serif;
  background: url('assets/background.png');
  height: 100vh;
}
</style>
