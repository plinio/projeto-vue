<template>
  <div class="corpo">
    <h1 class="centralizado">{{titulo}}</h1>
    <input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="filtre por parte do titulo">
    
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto">

        <meu-painel :titulo="foto.titulo">
          <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
        </meu-painel>

      </li>
    </ul>
    
  </div>

</template>

<script>

import Painel from './components/shared/painel/Painel.vue';

export default {

  components: {

    'meu-painel': Painel
  },

  data(){

    return {

      titulo: "AluraPic",
      fotos: [],
      filtro: ''
    }
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        // filtra a lista
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        // se o campo estiver vazio, não filtramos, retornamos a lista
        return this.fotos;
      }
    }
  }
  ,
  created(){

    let promise = this.$http.get("http://localhost:3000/v1/fotos");
    promise
      .then(res => res.json())
      .then(fotosApi => this.fotos = fotosApi, err => console.log(err));


  }

}
</script>

<style>

.corpo{
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: 0 auto;
}

.centralizado{
  text-align: center;
}

.lista-fotos{
  list-style: none;
}

.lista-fotos .lista-fotos-item{
  display: inline-block;
}

.imagem-responsiva {
  width: 100%;
}

.filtro{
  display: block;
  width: 100%;
}

</style>
