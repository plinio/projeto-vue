<template>
  <div>
    <h1 class="centralizado">{{titulo}}</h1>
    <p v-show="mensagem" class="centralizado">{{mensagem}}</p>
    <input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="filtre por parte do titulo">
    
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto">

        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva v-meu-transform="{incremento: 20, animate: true}" :url="foto.url" :titulo="foto.titulo"></imagem-responsiva>
          <meu-botao 
            tipo="button" rotulo="Remover" 
            v-on:botaoAtivado="remove(foto)"
            :confirmacao="true"
            estilo="perigo" />
        </meu-painel>

      </li>
    </ul>
    
  </div>

</template>

<script>

import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';

export default {

  components: {

    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva,
    'meu-botao': Botao
  },

  data(){

    return {

      titulo: "AluraPic",
      fotos: [],
      filtro: '',
      mensagem: ''
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
  },

  methods: {
    remove(foto){
      
      this.$http.delete(`v1/fotos/${foto._id}`)
        .then(()=> {
          
          let indice = this.fotos.indexOf(foto);
          this.fotos.splice(indice, 1); //remove o item do array
          this.mensagem = 'Foto removida com sucesso';
          }
          , err => {
            console.log(err);
            this.mensagem = 'Não foi possível remover a foto';
        } )
    }

  },

  created(){

    let promise = this.$http.get("v1/fotos");
    promise
      .then(res => res.json())
      .then(fotosApi => this.fotos = fotosApi, err => console.log(err));


  }

}
</script>

<style>

.centralizado{
  text-align: center;
}

.lista-fotos{
  list-style: none;
}

.lista-fotos .lista-fotos-item{
  display: inline-block;
}

.filtro{
  display: block;
  width: 100%;
}

</style>
