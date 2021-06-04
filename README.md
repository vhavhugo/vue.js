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
