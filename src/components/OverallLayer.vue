<template>
  <div>
    <div><h4 id="test-anchor" class="col-lg-8">{{overallLayerText}}</h4></div>
    <div>
      <img v-bind:src="this.getImgUrl(this.host , this.file)" alt="this.text1"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'overall-layer',
  data () {
    return {
      host: 'https://web.sgh.waw.pl/~gkoloch',
      file: '/koloch_talk.png',
      full: this.host + this.file,
      overallLayerText: 'W warstwie całościowej przyjrzymy się całościowej analizie vintage, ' +
        'bez podziału na zmienne, grupy, czy też możliwe okresy vin.',
      /* vinIlosciowyPath: '.data/1_all_act_act_age.PNG', */
      vinIlosciowyPath: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTvzkUp5wqiicRLX4KjzbO5pllFPxyWjxiBuwN-x1fSa53zbhTq',
      vinIlosciowyAsPath: 'D:\\Repos\\sas-raport\\data\\vin_ilosciowy_as.PNG',
      vinKwotowyPath: 'D:\\Repos\\sas-raport\\data\\vin_kwotowy.PNG',
      vinKwotowyAsPath: 'D:\\Repos\\sas-raport\\data\\vin_kwotowy_as.PNG',
      text1: 'dupa1'
    }
  },
  methods: {
    getImgUrl (hostVar, fileVar) {
      return (hostVar + fileVar).toString()
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
