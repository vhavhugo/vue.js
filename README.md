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
