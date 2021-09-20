# instalação

- Necessário ter o Nodejs instalado.
- extension no visual studio code vscode-vue

# instalar vue-cli
npm install vue-cli@2.7.0 -g  //-g = é globalmente

# O vue.js possue o CLI Command Line Interface

# instalar novo projeto
 - vue init webpack-simple alurapic
 - cd alurapic
 - npm install
 - npm run dev

# index.html
# Esse arquivo não existe, ele usa a pasta src em tempo de execução para acelerar o processo
<script src="/dist/buil.js"></script>  

# package.json
# Babel = é um transpiler
# Webpack = é um module bundler

# main.js
# Global View Object
import Vue from 'vue'


# interpolação
<h1>{{ titulo }}</h1>

# Esse não pode interpolar
<img v-bind:src="foto.url" v-bind:alt="foto.titulo">

# outra forma
<template>
  <div>
    <h1 v-text="titulo"></h1>
    <img :src="foto.url" :alt="foto.titulo">
  </div>
</template>
<script>
  export default {
    data() {
      return {
        titulo: 'Alurapic';
        fotos1: {
          url: 'https://==='
        },
        {
        foto2: {
          url: 'https://---',
          titulo: 'cachorro'
        }
      }
    }
  }
}
</script>

# -------------------------------------------------

<template>
  <div>
    <h1>{{ titulo }}</h1>
    <li v-for="foto as fotos">
      <img :src="foto.url" :alt="foto.titulo">
  </div>
</template>
<script>
  export default {
    data() {
      return {
        titulo: 'Alurapic';
        foto: [
          {
            url: 'https:// ====',
            titulo: 'cachorro'
          },
          {
            url: 'https:// ----',
            titulo: 'cachorrão'
          }
        ]
      }
    }
  }
}
</script>

# ---------------------------------------------------

# dentro da pasta api
npm run start

# Dentro da alurapic
# Esse modulo que não faz parte do vue-cli
npm install vue-resource@1.0.3 --save

# Dentro do main.js
import VueResource from 'vue-resource';
Vue.use(VueResource);

 # Instalar VueResource - dentro da pasta alurapic
 - npm install vue-resource@1.0.3 --save
 
 # /src/main.js
 - import VueResource from 'vue-resource';
 - Vue.use(VueResource);

# Lifecycle Hooks
# Criar componentes
<script>
export default {
  data() {
    return {
    }
  },
  created() {
    alert('Criei o componentes');
  }
}
</script>

# saber mais
https://vuejs.org/v2/api/#Options-Lifecycle-Hooks

# Pegando os dados da API
# $http e promises
<script>
export default {
  data() {
    return {
      titulo: 'Alurapic',
      fotos: []
    }
  },
  created() {
    let promise = this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>

# 04. Criando componentes e encapsulamentos

# Estilizando componente

<template>
  <div class="corpo">
    <h1 class="centralizado">{{ titulo }}</h1>
      <ul class="lista-fotos">
        <li class="lista-fotos-item" v-for="foto of fotos">
          <img :src="foto.url" :alt="foto.titulo">
        </li>
      </ul>
  </div>
</template>

<script>
export default {

  data() {

    return {
      titulo: 'Alurapic',
      fotos: []
    }
  },
  created() {
    let promise = this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>

<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }

  .centralizado {
    text-align: center;    
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }
</style>

# Modificando o estilo

<template>
  <div class="corpo">
    <h1 class="centralizado">{{ titulo }}</h1>

      <ul class="lista-fotos">
        <li class="lista-fotos-item" v-for="foto of fotos">
          <div class="painel">
            <h2 class="painel-titulo">{{ foto.titulo }}</h2>
            <div class="painel-conteudo">
              <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
            </div>
          </div>
        </li>
      </ul>
  </div>
</template>

<script>
export default {

  data() {

    return {
      titulo: 'Alurapic',
      fotos: []
    }
  },
  created() {
    let promise = this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>

<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }

  .centralizado {
    text-align: center;    
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .imagem-responsiva {
    width: 100%;
  }

    /* estilo do painel */ 

   .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }
</style>

# Fazendo funcionar o component e estilos

# App.vue

<template>
  <div class="corpo">
    <h1 class="centralizado">{{ titulo }}</h1>
      <ul class="lista-fotos">
        <li class="lista-fotos-item" v-for="foto of fotos">
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
    'meu-painel' : Painel
  },
  data() {
    return {
      titulo: 'Alurapic',
      fotos: []
    }
  },
  created() {
    let promise = this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>
<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }
  .centralizado {
    text-align: center;    
  }
  .lista-fotos {
    list-style: none;
  }
  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }
  .imagem-responsiva {
    width: 100%;
  }
</style>

# C:\xampp\htdocs\vue.js\alurapic\src\components\shared\painel\Painel.vue

<template>
  <div class="painel">
    <h2 class="painel-titulo">{{ titulo }}</h2>
      <slot class="painel-conteudo"></slot>
  </div>
</template>
<script>
export default {
    props: ['titulo']
 }
</script>

<!-- scoped = serve para encapsular o css no component -->
<style scoped>

    /* estilo do painel */ 

   .painel {
    padding: 0 auto;
    border: solid 2px grey;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }

  .painel .painel-titulo {
    text-align: center;
    border: solid 2px;
    background: lightblue;
    margin: 0 0 15px 0;
    padding: 10px;
    text-transform: uppercase;
  }

  * {
    box-shadow: 5px 5px 5px;
  }
</style>

# Filtrando
# v-on = diretiva do vue é do tipo onclick
# v-on:input = indica que é no input
# $event.target.value = pega o valor do evento, dispara toda vez que estou digitando
# A diretiva v-bind realiza uma associação que flui da fonte de dados para a view. Qualquer mudança na fonte de dados fará com que a view seja atualizada para representar o novo valor. Já a diretiva v-on realiza uma associação de evento que flui da view para a fonte de dados. Para que as mudanças realizadas por v-on sejam atualizadas na view, é necessário combinar v-on com v-bind.
# data bindings que vai do html para a vue

<input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="filtre por parte do título">

# A medida que eu vou digitando mostra no filtro interpolado, é um data bindings que vai da vue para o html
{{ filtro }}

export default {

  data() {

    return {
      titulo: 'Alurapic',
      fotos: [],
      filtro: ''
    }
  },

}

# Filtro concluido - App.vue

<template>
  <div class="corpo">

    <h1 class="centralizado">{{ titulo }}</h1>

    <input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="filtre pelo título da foto">

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
        </meu-painel>
      </li>
    </ul>

  </div>
</template>

<script>

import Painel from './components/shared/painel/Painel.vue'

export default {

  components: {

    'meu-painel': Painel
  },

  data () {
    return {
      titulo: 'Alurapic', 

      fotos: [],

      filtro: ''
    }
  },

  computed: {

    fotosComFiltro() {

      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }

    }
  },

  created() {

    this.$http
      .get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>
<style>

  .centralizado {
    text-align: center;
  }

  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .imagem-responsiva {
    width: 100%;
  }

  .filtro {
    display: block;
    width: 100%;
  }
</style>

# v-show = ganha um display none;

# mais um componente

Vamos criar o arquivo alurapic/src/components/shared/imagem-responsiva/ImagemResponsiva.vue:

<template>
    <img class="imagem-responsiva" :src="url" :alt="titulo">
</template>

<script>

export default {
    props: ['url', 'titulo']
}

</script>

<style scoped>
    .imagem-responsiva {
        width: 100%;
    }
</style>

Agora, vamos importar nosso componente em App.vue e utilizá-lo no lugar da tag img. Aliás, não esqueça de remover o estilo de App que movemos para dentro do nosso componente:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <h1 class="centralizado">{{ titulo }}</h1>

    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre pelo título da foto">

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
        </meu-painel>
      </li>
    </ul>

  </div>
</template>

<script>

import Painel from './components/shared/painel/Painel.vue';
import ImagemResponsiva from './components/shared/imagem-responsiva/ImagemResponsiva.vue'

export default {

  components: {

    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva
  },

  data () {
    return {
      titulo: 'Alurapic', 

      fotos: [],

      filtro: ''
    }
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {

    this.$http
      .get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos);
  }
}
</script>
<style>

  .centralizado {
    text-align: center;
  }

  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display: block;
    width: 100%;
  }
</style>

Neste capítulo aprendemos:

a diretiva v-on e como lidar com eventos do JavaScript
atalho para diretiva v-on
diferença de v-on para v-bind
a filtrar uma lista
compreender o uso de computed property
que podemos acessar qualquer propriedade de data através de this
a diretiva v-show
detalhe entre v-show e slots
como realizar transições com auxílio do componente transition
a criar mais um componente

# Configurando rotas

// alurapic\src\main.js

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';
import { routes } from './routes';

Vue.use(VueResource);
Vue.use(VueRouter);

const router = new VueRouter({ 
  routes, 
  mode: 'history'
});

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})

// alurapic\src\routes.js

import Cadastro from './components/cadastro/Cadastro.vue';
import Home from './components/home/Home.vue';

export const routes = [
    {path: '', component: Home},
    {path: 'cadastro', component: Cadastro}
];

// alurapic\src\App.vue
<template>
  <div class="corpo">
    <router-view></router-view>
  </div>
</template>

<script>
export default {

}
</script>
<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }
</style>

// alurapic\src\components\home\Home.vue

<template>
  <div>

    <h1 class="centralizado">{{ titulo }}</h1>

    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre pelo título da foto">

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
        </meu-painel>
      </li>
    </ul>

  </div>
</template>

<script>

import Painel from '../shared/painel/Painel.vue'
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue'

export default {

  components: {

    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva
  },

  data () {
    return {
      titulo: 'Alurapic', 

      fotos: [],

      filtro: ''
    }
  },

  computed: {

    fotosComFiltro() {

      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }

    }
  },

  created() {

    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>
<style>

  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display: block;
    width: 100%;
  }
</style>

# Martinez seguiu os seguintes passos para ativar um sistema de rotas em sua Single Page Application:

1) Baixou através do npm o módulo VueRouter registrando-o na aplicação logo em seguida.

2) Criou o arquivo src/routes.js no qual todas as rotas da aplicação são definidas. Vejamos seu arquivo:

// src/routes.js

import Componente1 from './components/componente1/Componente1.vue';
import Componente2 from './components/componente2/Componente2.vue';

export const routes = [

    { path: '/c1', componente: Componente1 },
    { path: '/c2', componente: Componente2 }

];COPIAR CÓDIGO
3) Em src/main.jsimportou o arquivo registrando-o no Global View Object:

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';

import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes, 
  mode: 'history'
});

Vue.use(VueResource);

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})COPIAR CÓDIGO
Tudo parece perfeito, mas há um erro em uma dessas etapas. Um erro sutil que pode acontecer com você. Consegue identificá-lo? Veja a resposta do instrutor logo em seguida.

VER OPINIÃO DO INSTRUTOR
Opinião do instrutor

O problema foi na hora de definir as rotas, ou seja, no passo 2:

export const routes = [

    { path: '/c1', componente: Componente1 },
    { path: '/c2', componente: Componente2 }

];COPIAR CÓDIGO
Veja que Martinez usou componente como nome da chave do objeto, quando na verdade deveria ser component. Esse pequeno deslize é capaz de invalidar a aplicação inteira.

Lembrando também, como default, sempre utilizar um path para url de entrada:

{path: '', component: Home},