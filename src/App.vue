<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Platzi Music
    h2 Seleccione un pais
    select(v-model="selectedPais")
      option(v-for="pais in paises" :value="pais.value") {{ pais.name }}
    spinner(v-show="loading")
    ul
      artista(v-for="artista in artistas" :artista="artista" :key="artista.mbid")
</template>

<script>
import Artista from './components/artista.vue';
import Spinner from './components/spinner.vue';
import getArtistas from './api';
export default {
  name: 'app',
  data () {
    return {
      artistas: [],
      paises: [
        { name: 'Venezuela', value: 'venezuela'},
        { name: 'Colombia', value: 'colombia'},
        { name: 'España', value: 'spain'}
      ],
      selectedPais: 'venezuela',
      loading: true
    }
  },

  components:{
    Artista,
    Spinner
  },
  methods:{
    refrescarArtistas(){
      const self = this;
      this.loading = true;
      this.artistas = [];
      getArtistas(this.selectedPais)
      .then(function(artistas) {
        self.artistas = artistas;
        self.loading = false;
      });
    }
  },

  mounted(){
    this.refrescarArtistas();
    },
  watch: {
    selectedPais(){
      console.log('cambios pais por:', this.selectedPais);
      this.refrescarArtistas();
    }
  }
}
</script>

<style lang="stylus">
  #app
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    margin-top 60px

  h1, h2
    font-weight normal

  ul
    list-style-type none
    padding 0

  li
    display inline-block
    margin 0 10px

  a
    color #42b983
</style>
