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

];
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
})
Tudo parece perfeito, mas há um erro em uma dessas etapas. Um erro sutil que pode acontecer com você. Consegue identificá-lo? Veja a resposta do instrutor logo em seguida.

VER OPINIÃO DO INSTRUTOR
Opinião do instrutor

O problema foi na hora de definir as rotas, ou seja, no passo 2:

export const routes = [

    { path: '/c1', componente: Componente1 },
    { path: '/c2', componente: Componente2 }

];
Veja que Martinez usou componente como nome da chave do objeto, quando na verdade deveria ser component. Esse pequeno deslize é capaz de invalidar a aplicação inteira.

Lembrando também, como default, sempre utilizar um path para url de entrada:

{path: '', component: Home},

# Criar component cadastro
# Vamos criá-lo em alurapic/src/components/cadastro/Cadastro.vue. Por enquanto será uma página simples, com apenas um título:

<!-- alurapic/src/components/cadastro/Cadastro.vue -->

<template>
  <div>
    <h1 class="centralizado">Cadastro</h1>
  </div>
</template>

<script>

export default {

}

</script>
<style scoped>
    .centralizado {
        text-align: center;
    }
</style>

# Para que o VueRouter saiba qual componente carregar precisamos registrar rotas para esses componentes. Rotas nada mais são que endereços especiais que são interceptados pelo VueRouter e a partir do endereço ele decidirá qual componente deve ser exibido em App que é o primeiro componente a ser exibido em nossa aplicação.

Vou estipular que os seguintes endereços serão válidos:

http://localhost:8080/#/   
http://localhost:8080/#/cadastro
O primeiro carregará o componente Home e o segundo o componente Cadastro. Você deve estar achando estranho o # no endereço. Ele é importante, porque eles fazem com que o browser não dispare uma requisição para o servidor, pois não é uma URL válida. No entanto, sendo algo totalmente válido para o VueRouter, ele extrairá a informação que vem logo após o # para saber qual componente carregar. Ele faz um dê para entre o pedaço da url que vem logo após o # com o seu respectivo componente.

Sendo assim, é uma boa prática declarar as rotas da aplicação em um arquivo em separado. Vamos criar o arquivo alurapic/src/routes.js. Nele exportaremos uma constante que um um array:

// alurapic/src/routes.js

export const routes = [
  /* rotas aqui */
];
Quando queremos exportar o valor de uma variável é necessário usar o prefixo const. Agora, vamos importar os componentes Home e Cadastro que equivalem a páginas:

// alurapic/src/routes.js

import Home from './components/home/Home.vue';
import Cadastro from './components/cadastro/Cadastro.vue';

export const routes = [
No array routes, precisamos ter um objeto Javascript com as propriedades path e component. O primeiro é a caminho que identifica o componente, o segundo o componente que será carregado para este caminho presente na url do navegador:

// alurapic/src/routes.js

import Home from './components/home/Home.vue';
import Cadastro from './components/cadastro/Cadastro.vue';

export const routes = [

    { path: '', component: Home },
    { path: '/cadastro', component: Cadastro }

];
Veja que para o componente Home usamos o path como uma string em branco. Esse é o padrão quando queremos acessar o componente como /#/. Já path do componente Cadastro é /cadastro que se traduzirá em uma URL como http://localhost:8080/#/cadastro.

Mas inda falta mais duas configurações. A primeira, é passar as rotas que configuramos para o VueRouter. Para isso, vamos importar routes de routes.js:

// alurapic/src/main.js

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';

// tem que vir entre chaves, porque não é default
import { routes } from './routes';

Vue.use(VueRouter);
Vue.use(VueResource);

new Vue({
  el: '#app',
  render: h => h(App)
})
Agora que importamos a rota, vamos criar uma instância de VueRouter passando como parâmetro um objeto JavaScript com a propriedade routes que deve receber como parâmetro as rotas que importamos. No caso, tanto a propriedade quando as rotas importadas possuem o mesmo nome:

// alurapic/src/main.js

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';

import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes : routes
});

Vue.use(VueResource);

new Vue({
  el: '#app',
  render: h => h(App)
})
Em ES6, quando o valor e a propriedade possuem o mesmo nome, podemos simplesmente fazer assim:

// alurapic/src/main.js

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';

import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes
});

Vue.use(VueResource);

new Vue({
  el: '#app',
  render: h => h(App)
})
Agora que temos efetivamente nossas rotas, precisamos passá-la como parâmetro para a view instance, aquela que renderiza nosso componente App:

// alurapic/src/main.js

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';

import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes : routes
});

Vue.use(VueResource);

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
Como o nome da propriedade tem o mesmo nome da nossa variável, podemos fazer apenas router ao invés de router: router.

Por fim, precisamos usar uma diretiva especial do VueRouter, uma que indica em que lugar do template de App os componentes serão carregados. Essa diretiva se chama router-view:

<!-- alurapic/src/App.vue -->
<template>
  <div class="corpo">

    <router-view></router-view>

  </div>
</template>

<script>
</script>

<style>

  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }
</style>
Quando o CLI rodando, veja que nossa aplicação será aberta automaticamente na URL http://localhost:8080/#/. Se quisermos acessar a página de cadastro, fazemos http://localhost:8080/#/cadastro.

Por fim, não há nada de errado com o # no endereço, é algo completamente válido e muito usado. No entanto, podemos removê-lo usando o modo history do VueRouter. No entanto, para este modo funcionar, seu backend que compartilha sua aplicação em Vue deve retornar sempre index.html para todos para qualquer endereço que chegar até ele, inclusive deve retornar index.html para páginas de erro. O Vue CLI já faz isso por padrão, mas se você for hospedar sua aplicação seja lá onde for, lembre-se desse detalhe.

Para ativarmos o modo history basta adicionarmos a propriedade mode com o valor history na instância de VueRouter.

import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource';
import VueRouter from 'vue-router';

import { routes } from './routes';

Vue.use(VueRouter);

// adicionando a propriedade mode com o valor history.

const router = new VueRouter({
  routes, 
  mode: 'history'
});

Vue.use(VueResource);

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
Veja que agora podemos acessar Home através de http://localhost:8080/ e Cadastro através de http://localhost:8080/cadastro. Esses endereços não dispararam uma requisição para o servidor e serão interceptados pelo VueRouter para saber qual componente carregar.

Fiz tudo direitinho, mas...
PRÓXIMA ATIVIDADE

Martinez seguiu os seguintes passos para ativar um sistema de rotas em sua Single Page Application:

1) Baixou através do npm o módulo VueRouter registrando-o na aplicação logo em seguida.

2) Criou o arquivo src/routes.js no qual todas as rotas da aplicação são definidas. Vejamos seu arquivo:

// src/routes.js

import Componente1 from './components/componente1/Componente1.vue';
import Componente2 from './components/componente2/Componente2.vue';

export const routes = [

    { path: '/c1', componente: Componente1 },
    { path: '/c2', componente: Componente2 }

];
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
})
Tudo parece perfeito, mas há um erro em uma dessas etapas. Um erro sutil que pode acontecer com você. Consegue identificá-lo? Veja a resposta do instrutor logo em seguida.

# O menu da aplicação
Vamos alterar alurapic/src/App.vue e adicionar um menu. Não vamos nos preocupar com estilização do menu, apenas um menu funcional para não perdemos o foco nesta parte tão importante:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <nav>
      <ul>       
          <li><a href="/">Home</a></li>
          <li><a href="/cadastro">Cadastro</a></li>
      </ul>
    </nav>

    <router-view></router-view>

  </div>
</template>
<script>
</script>
<style>

  /* código omitido */

</style>
Nosso menu é exibido e quando clicamos no link Cadastro somos direcionados para o componente Cadastro. Mas nem tudo esta perfeito. Veja que nossas navegações estão disparando o carregamento da página. Se estamos em uma Single Page Application, isso não deveria acontecer, pois já temos tudo o que precisamos carregado. O problema esta no uso da tag a para realizar a navegação. Para resolver esse problema, precisamos usar o componente router-link:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <nav>
      <ul>       
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/cadastro">Cadastro</router-link></li>
      </ul>
    </nav>

    <router-view></router-view>

  </div>
</template>
<script>
</script>
<style>

  /* código omitido */

</style>
Agora sim! Veja que a página não recarregando enquanto clicamos nos itens do menu. Muito melhor! No entanto, se olharmos o arquivo alurapic/src/routes.js já temos a lista com todas as rotas definidas nesse arquivo. Lá temos o path de cada rota, mas não temos o título. Não tem problema, vamos adicionar a propriedade titulo no array de routes. Isso não causará nenhum erro devido a natureza dinâmica do JavaScript e nos permitirá importar esse array para criar nosso menu dinamicamente. Toda vez que uma nova rota for adicionada em routes, automaticamente ela aparecerá como item do menu:

// alurapic/src/routes.js

import Home from './components/home/Home.vue';
import Cadastro from './components/cadastro/Cadastro.vue';

// adicionando a propriedade título

export const routes = [

    { path: '', component: Home, titulo: 'Home' },
    { path: '/cadastro', component: Cadastro, titulo: 'Cadastro' }

];
Agora, importando routes em App e disponibilizando a lista de rotas através da função data. Ah, desta vez vamos usar in no lugar de for na diretiva v-for. Eu prefiro of, mas se você vem do Angular 1 pode preferir o in:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <nav>
      <ul>       
          <li v-for="route in routes">
            <router-link :to="route.path ? route.path : '/'">{{route.titulo}}</router-link>
          </li>
      </ul>
    </nav>

     <router-view></router-view>

  </div>
</template>
<script>

import { routes }  from './routes';

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
    margin: 0 auto;
    width: 96%;
  }
</style>
Vocês devem estar estranhando a linha <router-link :to="route.path ? route.path : '/'">{{route.titulo}}</router-link>. Precisamos testar essa condição, porque o path de Home é um string vazia, mas quando usamos no componente router-link precisamos usar um /. Aliás, nosso menu é um forte candidato para se tornar um componente, mas não faremos isso agora.

# Animando transições de página

Uma das coisas mais bonitas do mundo da programação é podermos aplicar com conhecimento já adquirido e aplicá-lo em outros contextos. No capítulo anterior aprendemos a trabalhar com transições. Se refletirmos por um instante, a saída de uma página para a outra é uma mudança de estado, logo, passível de animação.

Vamos aplicar a mesma transição que fizemos com o componente Painel com a única diferença que será executada mais rapidamente. Aprendemos que precisamos envolver o componente desejado como alvo da transição através da tag transition. Sendo assim, qual componente você acha que devemos envolver para conseguir realizar transições entre páginas? O componente router-view em App!.

Alterando App:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <nav>
    <ul>    
      <li v-for="route in routes">
        <router-link :to="route.path ? route.path : '/'">
          {{route.titulo}}
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

import { routes }  from './routes';

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
    margin: 0 auto;
    width: 96%;
  }

  .pagina-enter-active, .pagina-leave-active {
    transition: opacity .3s
  }
  .pagina-enter, .pagina-leave-active {
    opacity: 0
  }
</style>
Veja que usamos os mesmos estilos, com a diferença que usamos como name do componente transitiono valor pagina e a transição foi reduzida para 200 milissegundos. Experimente clicar nos itens do menu da aplicação e veja a transição entre páginas sendo realizada. Se você domina CSS pode aplicar transições mais elaboradas, o mais importante é saber como integrá-las ao Vue.

# Transformando o menu em componente

Não precisamos meditar muito para ver que há algumas regrinhas para a criação do nosso menu, por isso ele é um forte candidado a ser tornar um componente em nossa aplicação. É exatamente isso que faremos.

Vamos criar o arquivo alurapic/src/components/shared/menu/Menu.vue. Ele receberá de um componente pai uma lista de rotas apenas. Vamos aproveitar e colocar uma validação dessa propriedade deixando explicito que aceitamos apenas o tipo Array:

<!-- alurapic/src/components/shared/menu/Menu.vue -->

<template>
    <nav>
      <ul>       
          <li v-for="rota in rotas">
            <router-link :to="rota.path ? rota.path : '/'">{{rota.titulo}}</router-link>
          </li>
      </ul>
    </nav>

</template>
<script>
export default {

    props: {
        rotas: {
            type: Array, 
            required: true
        }
    }
}
</script>    

<style scoped>
</style>
Eu preferi chamar internamente de rota ao invés de routes para não confundir com o array de rotas que se chama routes. Mas nada impede que vocês utilizem o mesmo nome.

Agora que temos nosso componente criado, vamos importá-lo em App, inclusive preciamos adicioná-lo na propriedade components para que seja acessível no template de App. Usaremos como nome meu-menu:

<!-- alurapic/src/App.vue -->

<template>
  <div class="corpo">

    <meu-menu :rotas="routes"/>

    <transition name="pagina">
      <router-view></router-view>
    </transition>

  </div>
</template>
<script>

import { routes }  from './routes';
import Menu from './components/shared/menu/Menu.vue';

export default {

  components: {
    'meu-menu' : Menu
  },

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
    margin: 0 auto;
    width: 96%;
  }

  .pagina-enter-active, .pagina-leave-active {
    transition: opacity .3s
  }
  .pagina-enter, .pagina-leave-active {
    opacity: 0
  }
</style>
Excelente, quando a página é recarregada tudo continua funcionando como antes. Agora que temos o menu isolado em um componente, fica mais fácil aplicar aquele estilo profissional ao menu. Mas isso eu deixarei para os meus alunos mestres em CSS.

# Neste capítulo aprendemos:

a criar um novo componente/página
o conceito de Single Page Application
extrair de App.vue um componente de página, separando responsabilidades
a baixar e registrar o módulo VueRouter
criar rotas da aplicação
o componente router-view
o modo history vs hash
a criar um menu baseado em nossas configurações de rota
a tornar o menu um componente
executar efeito de transição na troca de páginas
a validar propriedades em um componente