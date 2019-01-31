<template>
  <div>
    <div><h4 id="test-anchor" class="col-lg-8">{{this.aggregatedLayerText}}</h4></div>
    <div class="container select-params col-md-8 align-content-center">
      <form>
        <div class="form-group row">
          <label for="dueAL" class="col-md-6 col-form-label">Określ due (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-2 btn btn-secondary " id="dueAL" v-model="dueAL">
            <option selected>1</option>
            <option>2</option>
            <option>3</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-typeAL" class="col-md-6 col-form-label">Typ protfela (kredyt gotówkowy czy raty
            produktu) </label>
          <select class="form-control col-md-2 btn btn-secondary" id="wallet-typeAL" v-model="walletTypeAL">
            <option selected>all</option>
            <option>css</option>
            <option>ins</option>
          </select>
        </div>
      </form>
      <div class="results" v-if="allValuesProvidedAL">
        <h4>Vintage / wykres asymptotyczny</h4><br>
        <img v-bind:src="this.getImgUrlForAL(this.hostAL, this.dueAL, 'vin_a' , this.walletTypeAL)" alt=""/>
        <br><h4>Vintage / wykres ilościowy</h4><br>
        <img v-bind:src="this.getImgUrlForAL(this.hostAL, this.dueAL, 'vin_i' , this.walletTypeAL)" alt=""/>
        <br><h4>Vintage / wykres kwotowy</h4><br>
        <img v-bind:src="this.getImgUrlForAL(this.hostAL, this.dueAL, 'vin_k' , this.walletTypeAL)" alt=""/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'overall-layer',
  data () {
    return {
      hostAL: 'https://s3.amazonaws.com/projektsas/projekt_all/',
      dueAL: '1',
      walletTypeAL: 'all',
      aggregatedLayerText: 'W warstwie zbiorczej zajmujemy się przedstawieniem raportów dla całego portfela, a także poszczególnych produktów: css i ins.' +
      ' Mając już obliczony vintage, jesteśmy w stanie przedstawić wykresy zarówno dla poszczególnych typów portfela, jak i dla vin 1, 2 i 3. '
    }
  },
  methods: {
    getImgUrlForAL (host, due, vinType, wallet) {
      return (host + due + '/' + wallet + '/' + vinType + '/Vin.png').toString()
    },

    allValuesProvidedAL: function () {
      return this.due !== '' &&
          this.walletType !== ''
    }
  }
}
</script>

<style scoped>
  .showGraph {
    padding-left: 10%;
    padding-right: 10%;
    margin-top: 2%;
    margin-bottom: 2%;
  }

  h4 {
    display: inline-block;
    text-align: center;
    word-wrap: break-word;
    font-size: larger;
    margin: 2%;
  }

  .results {
    margin-top: 10%;
  }

  img {
    height: 75%;
    width: 75%;
    margin: 3%;
    display: inline-block;
    text-align: center;
  }

  label {
    text-align-all: left;
  }
</style>
