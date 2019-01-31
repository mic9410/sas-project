<template>
  <div class="vertical-center">
    <div class="page-container">
      <div class="item active">
        <img src="./../../img/dollar.jpg" alt="" width="2000" height="300"/>
        <!-- Opis slajdu -->
      </div>
      <h1>{{this.header}}</h1>
      <h2 class="col-lg-8">{{this.msg}}</h2>
      <div>
        <button-group class="col-md-8">
          <button class="btn btn-info btn-lg" v-on:click="visibleContainer = 1">Warstwa Zbiorcza</button>
          <button class="btn btn-info btn-lg" v-on:click="visibleContainer = 2">Warstwa Identytfikacji Zmiennych</button>
          <button class="btn btn-info btn-lg" v-on:click="visibleContainer = 3">Warstwa Zmiennych</button>
        </button-group>
      </div>
      <aggregate-layer v-if="visibleContainer === 1"></aggregate-layer>
      <overall-layer v-if="visibleContainer === 2"></overall-layer>
      <variable-layer v-if="visibleContainer === 3"></variable-layer>
      <br>
    </div>
  </div>
</template>

<script>
import AggregateLayer from './AggregateLayer'
import VariableLayer from './VariableLayer'
import OverallLayer from './OverallLayer'
import ButtonGroup from 'bootstrap-vue/es/components/button-group/button-group'
import Button from 'bootstrap-vue/es/components/button/button'

export default {
  components: {
    Button,
    ButtonGroup,
    AggregateLayer,
    OverallLayer,
    VariableLayer
  },

  name: 'introduction',

  data () {
    return {
      visibleContainer: 3,
      header: 'Raport podsumowujący prace nad projektem z przedmiotu SAS.',
      msg: 'Dla każdej z warstw otrzymujemy wykresy z informacjami, dotyczącymi analizy vintage kwotowego i ilościowego.'
    }
  }
}
</script>

<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  h2 {
    display: inline-block;
    text-align: center;
    word-wrap: break-word;
  }

  .btn-info {
    padding: 2%;
    margin-top: 2%;
    margin-bottom: 2%;
  }

</style>
