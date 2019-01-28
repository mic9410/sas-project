<template>
  <div>
    <div><h4 class="col-lg-8">{{overallLayerText}}</h4></div>
    <div>
     <img v-bind:src="vinIlosciowyPath" v-bind:alt="this.text1"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'overall-layer',
  data () {
    return {
      overallLayerText: 'W warstwie całościowej przyjrzymy się całościowej analizie vintage, ' +
        'bez podziału na zmienne, grupy, czy też możliwe okresy vin.',
      vinIlosciowyPath: '.data/1_all_act_act_age.PNG',
      vinIlosciowyAsPath: 'D:\\Repos\\sas-raport\\data\\vin_ilosciowy_as.PNG',
      vinKwotowyPath: 'D:\\Repos\\sas-raport\\data\\vin_kwotowy.PNG',
      vinKwotowyAsPath: 'D:\\Repos\\sas-raport\\data\\vin_kwotowy_as.PNG',
      text1: 'dupa1'
    }
  }
}
</script>

<style scoped>
  h4 {
    display: inline-block;
    text-align: center;
    word-wrap: break-word;
    font-size: larger;
    margin: 2%;
  }
</style>
