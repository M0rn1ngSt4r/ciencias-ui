
<template lang="pug">
  .pruebaContenedor.w-100.center
    h1 {{ msg }}
    p {{ descripcion }}
    #listaEventos.center.pa2-l.pa1 
      div.evento(v-for="evento in listaEventos")
        p {{evento.id}} {{ evento.titulo }}
            span {{ evento.fecha }}
        p {{ evento.ubicacion }}
    div
      h1 {{ msg2 }}
      p {{ descripcion2 }}
        ul
          li(v-for="evento in listaEventos")
            p(class = 'title') {{ evento.titulo }}
              span {{ evento.fecha }}
            p(class = 'event') {{ evento.ubicacion }}
    div
      h1 {{ msg3 }}
      p {{ descripcion3 }}
        ul
          li(v-for="evento in listaEventos")
            img(:src = "getImgPath(evento.imagen)")
            p(class = 'title') {{ evento.titulo }}
              span {{ evento.fecha }}
            p(class = 'event') {{ evento.ubicacion }}
</template>

<script>
import dataJson from '@/assets/data/eventos.json'

export default {
  name: 'Eventos',
  data () {
    return {
      dataJ: '',
      listaEventos: '',
      msg: 'Patrón de Lista',
      descripcion: 'El patrón list, En lugar de utilizar el espacio horizontal de manera ineficiente, muestra un conjunto de información verticalmente utilizando el espacio asignado completo.',
      msg2: 'Esquema 1',
      descripcion2: 'Implementar una lista vertical con la información de los eventos UNAM',
      msg3: 'Esquema 2',
      descripcion3: 'Consiste en agregar una imagen de tipo thumbnail representativa del evento.',
    }
  },
  methods: {
    setDataJ: function() {
      this.dataJ = dataJson
      console.log("dataJson ", this.dataJ ) 
    },  
    setListaEventos: function() {
      this.listaEventos = this.dataJ['eventos']
    },
    getImgPath: function(partial) {
      return '@/assets/images/' + partial;
    }
  },
  mounted(){
    this.setDataJ();
    this.setListaEventos();
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
      border:0.5px solid $black;
    }
    ul{
      padding: 0;
      list-style-type: none;
    }
    li{
      margin-top: 3px;
      margin-bottom: 3px;
      padding: 0;
      border: 2px solid $light-gray;
    }
    p{
      .title{
        color: $navy;
        font-weight: 900;
      }
      .event{
        color: $near-black;
        font-size: 80%;
      }
    }
    span{
      color: $blue;
      font-weight: 450;
      margin-left: 20px;
      font-size: .6em;
    }
  }
</style>
