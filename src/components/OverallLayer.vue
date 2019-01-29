<template>
  <div>
    <div><h4 id="test-anchor" class="col-lg-8">{{overallLayerText}}</h4></div>
    <div>
      <form>
      <select class="form-control col-md-2 btn btn-secondary " id="katalog" v-model="catalog">
        <option selected>1</option>
        <option>2</option>
        <option>3</option>
      </select>
        URL2: {{this.getImgUrl(this.host, this.catalog, this.file)}}
      </form>
      <img v-bind:src="this.getImgUrl(this.host, this.catalog, this.file)" alt="this.text1"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'overall-layer',
  data () {
    return {
      host: 'https://s3.amazonaws.com/projektsas/produkty_projektu/',
      file: '/vin1.jpg',
      catalog: '1',
      vinNumber: '1',
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
    getImgUrl (host, catalog, file) {
      return (host + catalog + file).toString()
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
