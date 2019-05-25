
<template lang="pug">
  .pruebaContenedor.w-100.center
    h1 {{ msg }}
    div(class='gallery')
      figure
        a(class='link', v-bind:href="listaImagenes[0].sitio") 
        img(v-bind:src="listaImagenes[0].url" )
        p(class='title') {{ listaImagenes[0].titulo }}
        p(class='location') {{ listaImagenes[0].ubicacion }}
      figure
        a(class='link', v-bind:href="listaImagenes[1].sitio") 
        img(v-bind:src="listaImagenes[1].url" )
        p(class='title') {{ listaImagenes[1].titulo }}
        p(class='location') {{ listaImagenes[1].ubicacion }}
      figure
        a(class='link', v-bind:href="listaImagenes[2].sitio") 
        img(v-bind:src="listaImagenes[2].url" )
        p(class='title') {{ listaImagenes[2].titulo }}
        p(class='location') {{ listaImagenes[2].ubicacion }}
      figure
        a(class='link', v-bind:href="listaImagenes[3].sitio") 
        img(v-bind:src="listaImagenes[3].url" )
        p(class='title') {{ listaImagenes[3].titulo }}
        p(class='location') {{ listaImagenes[3].ubicacion }}
      figure
        a(class='link', v-bind:href="listaImagenes[4].sitio") 
        img(v-bind:src="listaImagenes[4].url" )
        p(class='title') {{ listaImagenes[4].titulo }}
        p(class='location') {{ listaImagenes[4].ubicacion }}
      figure
        a(class='link', v-bind:href="listaImagenes[5].sitio") 
        img(v-bind:src="listaImagenes[5].url" )
        p(class='title') {{ listaImagenes[5].titulo }}
        p(class='location') {{ listaImagenes[5].ubicacion }}
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
    p{
      &.title{
        color: $navy;
        font-weight: 900;
      }
      &.location{
        color: $near-black;
        font-weight: 600;
        font-size: 80%;
      }
    }
    img{
      border: 5px solid $gold;
      border-radius: 4px;
      width: 100%;
      height: auto;
      object-fit: cover;
      display: block;
    }
    figure{
      position: relative;
      border-right: 3px solid #dfdfdf;
      padding-right: 35px;
      margin-left: 10px;
      margin-right: 0px;
      padding-left: 15px;
    }
    a{
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 100%;
    }
  }
</style>
