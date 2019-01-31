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
          <select class="form-control col-md-2 btn btn-secondary" id="variable-category-type" v-model="categoryType">
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
                    v-if="categoryType === 'ACT'">
              <option v-for="variable in bestVariables.ACT">{{variable}}</option>
            </select>
            <select class="form-control  btn btn-secondary"
                    v-model="variableName"
                    v-if="categoryType === 'AGR'">
              <option v-for="variable in bestVariables.AGR">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="categoryType === 'APP'">
              <option v-for="variable in bestVariables.APP">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="categoryType === 'AGS'">
              <option v-for="variable in bestVariables.AGS">{{variable}}</option>
            </select>
          </div>
        </div>
      </form>
      <div class="results" v-if="allValuesProvided">
        Wartości dla klasy: {{ this.getCategories(this.variableName, 1).war }} <br>
        <img
          v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.categoryType, this.getVariablePosition(this.categoryType, this.variableName), 1)"
          alt=""/>
        <br>
        Wartości dla klasy: {{ this.getCategories(this.variableName, 2).war }} <br>
        <img
          v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.categoryType, this.getVariablePosition(this.categoryType, this.variableName), 2)"
          alt=""/>
        <br>
        Wartości dla klasy: {{ this.getCategories(this.variableName, 3).war }} <br>
        <img
          v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.categoryType, this.getVariablePosition(this.categoryType, this.variableName), 3)"
          alt=""/>
      </div>
    </div>
  </div>
</template>

<script>
import {categoriesArr} from './../../data/categoriesArr'

export default {
  name: 'variable-layer',
  data () {
    return {
      bestVariables: {
        ACT: [
          'ACT9_N_GOOD_DAYS',
          'ACT6_N_GOOD_DAYS',
          'ACT3_N_GOOD_DAYS',
          'ACT_CALL_N_LOAN',
          'ACT_CCSS_N_LOAN'],
        AGR: [
          'AGR3_MAX_CMAXI_DAYS',
          'AGR9_MAX_CMAXC_DUE',
          'AGR6_MAX_CMAXA_DUE',
          'AGR6_MAX_CMAXC_DAYS',
          'AGR6_MAX_CMAXA_DAYS'
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
      due: '1',
      walletType: 'all',
      categoryType: 'ACT',
      variableName: 'ACT_CALL_N_LOAN',
      variableNumber: this.getVariablePosition(this.categoryType, this.variableName),
      variableLayerText: 'W warstwie zmiennych przyjrzmy się bliżej, jaki wpływ na ostateczny rezultat mają pojedyncze zmienne. ' +
        'Z każdej kategorii wybieramy pięć najlepszych na podstawie wartości współczynnika Ginie\'go.'
    }
  },
  methods: {
    allValuesProvided: function () {
      return this.due !== '' &&
          this.walletType !== '' &&
          this.categoryType !== '' &&
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

    getCategories (variableName = 'ACT9_N_GOOD_DAYS', group = 1) {
      return categoriesArr.find(x => x.zmienna === variableName && x.grp === group)
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
