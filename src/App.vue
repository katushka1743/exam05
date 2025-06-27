<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template >
  <div class="template">
    <header>
      <h1>Ресторан "Берег моря"</h1>
    </header>
    <main class="main">
        <HelloWorld />
    </main>
    <footer>
      <a href="tel:+78005553535">8 (800) 555-35-35</a>
      <p>&#169; 2025 год</p>
    </footer>
  </div>

</template>

<style scoped>

.template {
  display: flex;
  flex-direction: column;
}

.main {
  flex-grow: 1;
  /* height: 100vh; */
}

header, footer {
  margin: 0;
  padding: 0;
}



</style>
