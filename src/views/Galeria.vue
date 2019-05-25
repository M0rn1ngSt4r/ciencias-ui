
<template lang="pug">
  .pruebaContenedor.w-100.center
    h1 {{ msg }}
    div(class='gallery')
      figure(v-bind:class="{border_right: ((i+1)%2)}" v-for="(imagen, i) in listaImagenes")
        a(v-bind:href="imagen.sitio") 
          img(v-bind:src="imagen.url" )
        a(class='title' v-bind:href="imagen.sitio") {{ imagen.titulo }}
        p(class='location') {{ imagen.ubicacion }}
</template>

<script>
import dataJson from '@/assets/data/galeria.json'

export default {
  name: 'Galeria',
  data () {
    return {
      dataJ: '',
      listaImagenes: '',
      msg: 'La UNAM Recomienda:',
    }
  },
  methods: {
    setDataJ: function() {
      this.dataJ=dataJson
      console.log("dataJson ", this.dataJ) 
    },  
    setListaImagenes: function() {
      this.listaImagenes=this.dataJ['eventos']
    }
  },
  mounted(){
    this.setDataJ();
    this.setListaImagenes();
  }

}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  lang="scss">
  //colors
  $cyan: #17a2b8 !default;
  //styles
  .pruebaContenedor{
    background-color: $white;
    border: 1px solid $black;
    .unamGoldColor.bold{
      font-weight: 900;
    }
    .unamGoldColor{
      color:$gold;
      &.bold{
        font-weight: 600;
      }
    }
    div{
      width: 80%;
      margin: 2rem auto; 
      border:0.5px solid $black;
      &.gallery {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
        grid-gap: 2 rem;
      }
    }
    .title{
      color: $navy;
      font-weight: 900;
      text-decoration: none;
    }
    .location{
      color: $near-black;
      font-weight: 600;
      font-size: 80%;
    }
    img{
      border: 5px solid $gold;
      border-radius: 4px;
      width: 100%;
      height: auto;
      max-height: 300px;
      object-fit: cover;
      display: block;
      margin-bottom: 25px;
    }
    figure{
      height: 375px;
      position: relative;
      padding-right: 35px;
      margin-left: 10px;
      margin-right: 0px;
      padding-left: 15px;
    }
    .border_right{
      border-right: 3px solid #dfdfdf;
    }
    a{
      width: 100%;
    }
  }
</style>
