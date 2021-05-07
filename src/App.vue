<template>
  <div class="corpo">

    <nav>
      <ul>       
          <!--<li><router-link to="/">Home</router-link></li>
          <li><router-link to="/cadastro">Cadastro</router-link></li>
          -->
          <li v-for="route in routes" :key="route">
              <router-link :to="route.path ? route.path : '/'">{{ route.titulo }}</router-link>
          </li>
      </ul>
    </nav>

    <router-view></router-view>
  </div>
</template>

<script>

import {routes} from './routes'

export default {

  data(){

    return{

      routes: routes
    }
  }
}

</script>

<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }
</style>