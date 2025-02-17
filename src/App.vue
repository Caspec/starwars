<template>
  <div class="d-flex flex-column min-vh-100">
    <HeaderComponent />
    <main class="container flex-grow-1 mt-4">
      <ContentComponent />
    </main>
    <FooterComponent />
  </div>
</template>


<script>
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import ContentComponent from './components/ContentComponent.vue';

export default {
  components: {
    HeaderComponent,
    FooterComponent,
    ContentComponent
  }
};
</script>

<style>
body {
  background-color: #000;
  color: yellow;
  font-family: 'Star Jedi', sans-serif;
  text-align: center;
}
</style>
