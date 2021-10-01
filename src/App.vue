<template>
  <div id="app">
    <div id="nav" v-if="usuario">
      <router-link to="/home">Home</router-link> |
       <!-- <router-link to="/cadastro">Criar usuário</router-link> | -->
      <router-link to="/historico-transferencias">Histórico de transação</router-link> |
      <router-link to="/transacao">Transação</router-link>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      usuario: ''
    }
  },
  mounted () {
    this.usuario = JSON.parse(localStorage.getItem('usuario'))
    console.log(this.usuario)
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}
#nav a {
  font-weight: bold;
  color: #2c3e50;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
