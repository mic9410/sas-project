/* eslint-disable vue/require-v-for-key */
<template>
  <div>
    <h4 class="col-lg-8">{{variableLayerText}}</h4>
    <div class="container select-params col-md-8 align-content-center">
      <form>
        <div class="form-group row">
          <label for="due" class="col-md-6 col-form-label">Określ due (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-2 btn btn-secondary " id="due" v-model="due">
            <option selected>1</option>
            <option>2</option>
            <option>3</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-type" class="col-md-6 col-form-label">Typ protfela (kredyt gotówkowy czy raty
            produktu) </label>
          <select class="form-control col-md-2 btn btn-secondary" id="wallet-type" v-model="walletType">
            <option selected>all</option>
            <option>css</option>
            <option>ins</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="variable-category-type" class="col-md-6 col-form-label">Kategoria zmiennej
            <a v-b-tooltip.hover="'ACT - w momencie pomiaru\n' +
            'AGR - kategorie zmiennych behawioralnych, gdzie missing w danych powoduje missing agregatu\n'+
            'APP - opisują klienta w momencie aplikacji\n'+
            'AGS - kategorie zmiennych behawioralnych'"
               variant="outline-success">
              <i class="fas fa-info-circle"></i>
            </a>
          </label>
          <select class="form-control col-md-2 btn btn-secondary" id="variable-category-type" v-model="grupa">
            <option selected>ACT</option>
            <option>AGR</option>
            <option>APP</option>
            <option>AGS</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-type" class="col-md-6 col-form-label">Wybierz jedną z top 5 najistotniejszych
            zmiennych</label>
          <div id="variableName" class="">
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="grupa === 'ACT'">
              <option v-for="variable in bestVariables.ACT">{{variable}}</option>
            </select>
            <select class="form-control  btn btn-secondary"
                    v-model="variableName"
                    v-if="grupa === 'AGR'">
              <option v-for="variable in bestVariables.AGR">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="grupa === 'APP'">
              <option v-for="variable in bestVariables.APP">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="grupa === 'AGS'">
              <option v-for="variable in bestVariables.AGS">{{variable}}</option>
            </select>
          </div>
        </div>

        <div class="results" v-if="allValuesProvided">
          <h4>Wartości dla klasy: {{ this.getCategories(this.due, this.walletType, this.grupa, this.variableName, 1).war }}</h4><br>
          <img
            v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.grupa, this.getGinni(this.due, this.walletType, this.grupa, this.variableName), 1)"
            alt=""/>
          <br>
          <h4>Wartości dla klasy: {{ this.getCategories(this.due, this.walletType, this.grupa, this.variableName, 2).war  }}</h4><br>
          <img
            v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.grupa, this.getGinni(this.due, this.walletType, this.grupa, this.variableName), 2)"
            alt=""/>
          <br>
          <h4>Wartości dla klasy: {{ this.getCategories(this.due, this.walletType, this.grupa, this.variableName, 3).war }}</h4>
          <img
            v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.grupa, this.getGinni(this.due, this.walletType, this.grupa, this.variableName), 3)"
            alt=""/>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import {categoriesArr} from './../../data/categoriesArr'
import {variablesArr} from './../../data/variablesArr'

export default {
  name: 'variable-layer',
  data () {
    return {
      bestVariables: {
        ACT: [
          'ACT_CCSS_N_LOAN',
          'ACT_CALL_N_LOAN',
          'ACT3_N_GOOD_DAYS',
          'ACT6_N_GOOD_DAYS',
          'ACT9_N_GOOD_DAYS'
        ],
        AGR: [
          'AGR6_MAX_CMAXA_DAYS',
          'AGR6_MAX_CMAXC_DAYS',
          'AGR6_MAX_CMAXA_DUE',
          'AGR9_MAX_CMAXC_DUE',
          'AGR3_MAX_CMAXI_DAYS'
        ],
        APP: [
          'APP_CHAR_JOB_CODE',
          'APP_INSTALLMENT',
          'APP_N_INSTALLMENTS',
          'APP_LOAN_AMOUNT',
          'APP_CHAR_BRANCH'
        ],
        AGS: [
          'AGS6_MAX_CMAXC_DAYS',
          'AGS3_MAX_CMAXA_DAYS',
          'AGS12_MAX_CMAXA_DAYS',
          'AGS9_MAX_CMAXA_DAYS',
          'AGS6_MAX_CMAXA_DAYS'
        ]
      },
      host: 'https://s3.amazonaws.com/projektsas/projekt_all/',
      due: 1,
      walletType: 'all',
      grupa: 'ACT',
      variableName: 'ACT6_N_GOOD_DAYS',
      variableNumber: this.getVariablePosition(this.grupa, this.variableName),
      variableLayerText: 'W warstwie zmiennych przyjrzmy się bliżej, jaki wpływ na ostateczny rezultat mają pojedyncze zmienne. ' +
        'Z każdej kategorii wybieramy pięć najlepszych na podstawie wartości współczynnika Ginie\'go.'
    }
  },
  methods: {
    allValuesProvided: function () {
      return this.due !== '' &&
          this.walletType !== '' &&
          this.grupa !== '' &&
          this.variableName !== ''
    },

    getVariablePosition: function (category, varName) {
      if (category === 'ACT') {
        return this.bestVariables.ACT.indexOf(varName) + 1
      }
      if (category === 'AGR') {
        return this.bestVariables.AGR.indexOf(varName) + 1
      }
      if (category === 'APP') {
        return this.bestVariables.APP.indexOf(varName) + 1
      }
      if (category === 'AGS') {
        return this.bestVariables.AGS.indexOf(varName) + 1
      }
    },

    getImgUrl (host, due, wallet, category, variable, classification) {
      return (host + due + '/' + wallet + '/' + category + '/' + variable + '/' + classification + '/Vin.png').toString()
    },

    getCategories (due1, walletType1, grupa1, zmienna1, klasa1) {
      if (categoriesArr.find(x => x.due === due1 && x.walletType === walletType1 && x.grupa === grupa1 && x.zmienna === zmienna1 && x.klasa === klasa1) === undefined) {
        return 'und'
      } else {
        return categoriesArr.find(x => x.due === due1 && x.walletType === walletType1 && x.grupa === grupa1 && x.zmienna === zmienna1 && x.klasa === klasa1)
      }
    },

    getGinni (due1, product1, grupa1, zmienna1) {
      if (variablesArr.find(x => x.dueOrVin === due1 && x.prod === product1 && x.grupa === grupa1 && x.zmienna === zmienna1) === undefined) {
        return ''
      } else {
        return variablesArr.find(x => x.dueOrVin === due1 && x.prod === product1 && x.grupa === grupa1 && x.zmienna === zmienna1).kolejnosc_wg_gini
      }
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

  img {
    height: 75%;
    width: 75%;
    margin: 3%;
    display: inline-block;
    text-align: center;
  }

  .results {
    margin-top: 10%;
  }

  label {
    text-align-all: left;
  }
</style>
