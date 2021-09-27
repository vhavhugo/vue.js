<template>
  <div class="corpo">
  <!-- Hora tem que exibir um componente, hora outro. -->
    <nav>
      <ul>
        <!-- <li><router-link to="/">Home</router-link></li> -->
        <!-- <li><router-link to="/cadastro">Cadastro</router-link></li> -->
          <li v-for="route in routes">
            <router-link :to="route.path ? route.path : '/'">
              {{ route.titulo }}
            </router-link>
          </li>
      </ul>
    </nav>
    <transition name="pagina">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>

import { routes } from './routes';

export default {
  data() {
    return {
      routes
    }
  }
}
</script>
<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }

  .pagina-enter, .pagina-leave-active {
    opacity: 0
  }

  .pagina-enter-active, .pagina-leave-active {
    transition: opacity .4s
  }
</style>