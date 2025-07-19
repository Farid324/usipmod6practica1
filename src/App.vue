<template>
  <div id="app">
    <router-view />
    <footer>
      <hr />
      <p>Práctica 1 - Agenda de Contactos | Vue 3 + JSON Server</p>
      <p>Desarrollado por: [Tu Nombre Aquí]</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: #f0f2f5;
  margin: 0;
  padding: 0;
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

footer {
  text-align: center;
  margin-top: auto;
  padding: 1rem;
  background-color: #ffffff;
  font-size: 14px;
}
</style>