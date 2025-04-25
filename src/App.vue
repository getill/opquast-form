<script setup lang="ts">
import Nav from "./components/Nav.vue";
import Form from './components/Form.vue'
import Footer from "./components/Footer.vue";
</script>

<template>
    <Nav />
    <main>
      <Form msg="Vite + Vue" />
    </main>
    <Footer />
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 100%;
  margin: 0;
  padding: 0;
}

main {
  flex: 1;
  /* width: 100%; */
  padding: 2rem;
}

#app {
  width: 100%;
  max-width: 100%;
  margin: 0;
  padding: 0;
}
</style>
