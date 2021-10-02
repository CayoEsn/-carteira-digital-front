<template>
  <div class="hello">

    <h2 v-if="usuario">Bem-Vindo {{ usuario.nome }}</h2>
    <h4>Seu saldo é de: R$ {{ formatPrice(saldo) }}</h4>

    <button @click='sair'>Sair</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'home',
  data () {
    return {
      usuario: null,
      saldo: 0
    }
  },
  mounted () {
    this.usuario = JSON.parse(localStorage.getItem('usuario'))
    this.buscarSaldo()
  },
  methods: {
    sair: function () {
      localStorage.removeItem('usuario')
      this.$router.replace('login')
    },
    buscarSaldo: function () {
      axios
        .get('https://carteira-digital-backend.herokuapp.com/saldo/saldo-usuario', { params: { login: this.usuario.login } })
        .then((response) => {
          this.saldo = response.data.saldo
        })
        .catch((error) => {
          return alert(error)
        })
    },
    formatPrice (value) {
      let val = (value / 1).toFixed(2).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
