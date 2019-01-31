<template>
  <div>
    <div><h4 id="test-anchor" class="col-lg-8">{{overallLayerText}}</h4></div>
    <div class="container select-params col-md-8 align-content-center">
      <form>
        <div class="form-group row">
          <label for="due" class="col-md-6 col-form-label">Określ due (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-2 btn btn-secondary " id="due" v-model="dueAL">
            <option selected>1</option>
            <option>2</option>
            <option>3</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-type" class="col-md-6 col-form-label">Typ protfela (kredyt gotówkowy czy raty
            produktu) </label>
          <select class="form-control col-md-2 btn btn-secondary" id="wallet-type" v-model="walletTypeAL">
            <option selected>all</option>
            <option>css</option>
            <option>ins</option>
          </select>
        </div>
        {{this.getImgUrl(this.hostAL, this.dueAL, 'vin_a' , this.walletTypeAL)}}
      </form>
      <div class="row align-items-center justify-content-center">
        <button v-on:click="displayResults" class="btn btn-info showGraph">Pokaż wykres</button>
      </div>
      <img v-bind:src="this.getImgUrl(this.hostAL, this.dueAL, 'vin_a' , this.walletTypeAL)" alt=""/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'overall-layer',
  data () {
    return {
      hostAL: 'https://s3.amazonaws.com/projektsas/produkty_projektu/',
      dueAL: '1',
      walletTypeAL: 'all',
      overallLayerText: 'W warstwie zbiorczej zajmujemy się '
    }
  },
  methods: {
    getImgUrl (host, due, vinType, wallet) {
      return (host + due + '/' + wallet + '/' + vinType + '/Vin.png').toString()
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
