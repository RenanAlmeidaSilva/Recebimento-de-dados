<template>
  <div id="app">
    <div class="card2">
      <dashboard
          nome="maquina - 1"
          nome-display="Machine 1"
      />
      &emsp;
      <dashboard
          nome="maquina - 2"
          nome-display="Machine 2"
      />
      &emsp;
      <dashboard
          nome="maquina - 3"
          nome-display="Machine 3"
      />
      &emsp;
      <dashboard
          nome="maquina - 4"
          nome-display="Machine 4"
      />
      <br><br>
      <dashboard
          nome="maquina - 5"
          nome-display="Em manutenção"
      />
      &emsp;
      <dashboard
          nome="maquina - 5"
      />
      &emsp;
      <dashboard
          nome="maquina - 5"
          nome-display="Em manutenção"
      />
      &emsp;
      <dashboard
          nome="maquina - 5"
          nome-display="Em manutenção"
      />
    </div>
  </div>
</template>


<script>
import Dashboard from "@/components/dashboard";

export default {
  name: 'App',
  components: {Dashboard},

  mounted() {
    this.$mqtt.subscribe('aut_lab/#')
  },
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 15px;
}

body {
  background-color: black;
  overflow: hidden;
}

.card2 {
  text-align: center;
  margin: auto;
}
</style>
