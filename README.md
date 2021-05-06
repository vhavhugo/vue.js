# instalação

- Necessário ter o Nodejs instalado.
- extension no visual studio code vscode-vue

# instalar vue-cli
npm install vue-cli@2.7.0 -g

# instalar novo projeto
 - vue init webpack-simple alurapic
 - cd alurapic
 - npm install
 - npm run dev

 # Instalar VueResource - dentro da pasta alurapic
 - npm install vue-resource@1.0.3 --save
 
 # /src/main.js
 - import VueResource from 'vue-resource';
 - Vue.use(VueResource);

# Filtrar a lista da API
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

