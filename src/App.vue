<template>
  <div>
    <h1>{{titulo}}</h1>
    <ul>
      <li v-for="foto of fotos" :key="foto">
        <img :src="foto.url" :alt="foto.titulo">
      </li>
    </ul>
    
  </div>

</template>

<script>
export default {
  data(){

    return {
      titulo: "AluraPic",
      fotos: [
        {
        url: "https://media.gazetadopovo.com.br/viver-bem/2018/11/dog3-768x587-0e01be20.jpg",
        titulo: "cachorro"
        },
        {
        url: "https://www.petz.com.br/blog/wp-content/uploads/2021/03/piercing-para-cachorro-2.jpg",
        titulo: "cachorro 2"
        },
      ]
    }

  }
}
</script>

<style>

</style>
