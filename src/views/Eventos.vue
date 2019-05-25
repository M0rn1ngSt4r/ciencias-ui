
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
      h1 {{ msg3 }}
      p {{ descripcion3 }}
        ul
          li(v-for="evento in listaEventos")
            img(v-bind:src = "getImgPath(evento.imagen)")
            p(class = 'title2') {{ evento.titulo }}
            p(class = 'fecha') {{ evento.fecha }}
            p(class = 'event') {{ evento.ubicacion }}
      h1 {{ msg4 }}
      p {{ descripcion4 }}
        ul
          li(v-for="evento in listaEventos")
            img(v-bind:src = "getImgPath(evento.imagen)")
            div(class = "date")
              span(class = "month start") de: {{ getStartMonth(evento.fecha) }}
              h1(class = "day") {{ getStartDay(evento.fecha) }}, {{ getStartHour(evento.fecha) }}
              span(class = "month end") a: {{ getEndMonth(evento.fecha) }}
              h1(class = "day") {{ getEndDay(evento.fecha) }}, {{ getEndHour(evento.fecha) }}
            p(class = 'title2') {{ evento.titulo }}
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
      images: null,
      msg: 'Patrón de Lista',
      descripcion: 'El patrón list, En lugar de utilizar el espacio horizontal de manera ineficiente, muestra un conjunto de información verticalmente utilizando el espacio asignado completo.',
      msg2: 'Esquema 1',
      descripcion2: 'Implementar una lista vertical con la información de los eventos UNAM',
      msg3: 'Esquema 2',
      descripcion3: 'Consiste en agregar una imagen de tipo thumbnail representativa del evento.',
      msg4: 'Esquema 3',
      descripcion4: 'Además de agregar una imagen de tipo thumbnail representativa del evento, se debe crear un elemento gráfico que represente la fecha del evento, como etiquetas de calendario.'
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
    loadImages: function() {
      this.images = require.context("../assets/images/eventos/", false, /\.jpg$/);
    },
    getImgName(partial) {
      return partial.split('\\').pop().split('/').pop();
    },
    getImgPath: function(partial) {
      return this.images("./" + this.getImgName(partial));
    },
    getStartMonth: function(date) {
      return date.split(",")[0].split(" ")[1].toUpperCase();
    },
    getEndMonth: function(date) {
      var aux = date.split("–");
      if (aux.length < 2) {
        return this.getStartMonth(date);
      }
      aux = aux[1].split(",");
      if (aux.length < 2) {
        return this.getStartMonth(date);
      } 
      return aux[0].split(" ")[2].toUpperCase();
    },
    getStartDay: function(date) {
      return date.split(",")[0].split(" ")[0];
    },
    getEndDay: function(date) {
      var aux = date.split("–");
      if (aux.length < 2) {
        return this.getStartDay(date);
      }
      aux = aux[1].split(",");
      if (aux.length < 2) {
        return this.getStartDay(date);
      } 
      return aux[0].split(" ")[1];
    },
    getStartHour: function(date) {
      return date.split("–")[0].split("las")[1];
    },
    getEndHour: function(date) {
      var aux = date.split("–");
      if (aux.length < 2) {
        return '–';
      } 
      aux = aux[1].split(" ");
      return aux[aux.length - 2] + " " + aux[aux.length - 1];
    },
  },
  mounted(){
    this.setDataJ();
    this.setListaEventos();
    this.loadImages();
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
      &.date {
        border: 5px solid $moon-gray;
        border-radius: 4px;
        float: left;
        display: block;
        width: 170px;
        height: 140px;
        margin: 15px 10px 10px 10px;
        text-align: center;
        font-family: sans-serif;
        position: relative;
      }
    }
    h1{
      &.day {
        display: block;
        margin: 0;
        padding: 10px;
        font-size: 20px;
        position: relative;
      }
    }
    ul{
      padding: 0;
      list-style-type: none;
      width: 70%;
      display:table; 
      margin:0 auto;
    }
    li{
      margin-top: 10px;
      margin-bottom: 10px;
      padding: 0;
      border: 2px solid $light-gray;
      overflow: auto;
      transform: scale(1);
      transition: transform 0.3s ease-out;
      &:hover{
        transform: scale(1.1);
        transition: transform 0.4s ease-in;
        transition: border-color .3s ease-in-out;
        border-color: $light-blue;
      }
    }
    p{
      &.title{
        color: $navy;
        font-weight: 900;
      }
      &.title2{
        color: $navy;
        font-size: 30px;
        font-weight: 1000;
      }
      &.fecha{
        color: $dgae-dark-gray2;
        font-weight: 450;
        font-size: .8em;
      }
      &.event{
        color: $near-black;
        font-weight: 600;
        font-size: 80%;
      }
    }
    span{
      color: $blue;
      font-weight: 450;
      font-size: .6em;
      margin-left: 20px;
      &.month {
        margin-left: 0px;
        display: block;
        color: $white;
        font-size: 18px;
        font-weight: bold;
        box-shadow: inset 0 -1px 0 0 #666;
      &.start{
          background: #406634;
        }
      &.end{
          background: #664134;
        }
      }
    }
    img{
      float: left;
      margin: 10px 10px 10px 10px;
      border: 5px solid $gold;
      border-radius: 4px;
      height: 150px;
    }
  }
</style>
