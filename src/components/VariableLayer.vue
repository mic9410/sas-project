/* eslint-disable vue/require-v-for-key */
<template>
  <div>
    <h4 class="col-lg-8">{{variableLayerText}}</h4>
    <div class="container select-params col-md-8 align-content-center">
      <form>
        <div class="form-group row">
          <label for="due" class="col-md-6 col-form-label">Określ due (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-2 btn btn-secondary " id="due" v-model="due">
            <option>1</option>
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
                    v-if="due === '1' && walletType === 'all' && grupa === 'ACT'">
              <option selected
                v-for="variable in ['ACT_CCSS_N_LOAN','ACT_CALL_N_LOAN','ACT3_N_GOOD_DAYS','ACT6_N_GOOD_DAYS', 'ACT9_N_GOOD_DAYS',]">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'css' && grupa === 'ACT'">
              <option selected
                v-for="variable in ['ACT_CCSS_N_STATB', 'ACT_CCSS_MIN_LNINST', 'ACT_CCSS_MIN_PNINST', 'ACT9_N_GOOD_DAYS','ACT12_N_GOOD_DAYS']">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'ins' && grupa === 'ACT'">
              <option  v-for="variable in ['ACT_CINS_N_STATB','ACT_CALL_ALL','ACT_CINS_ACP','ACT_LOANINC','ACT_CC']">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'all' && grupa === 'AGR'">
              <option
                v-for="variable in ['AGR6_MAX_CMAXA_DAYS', 'AGR6_MAX_CMAXC_DAYS', 'AGR6_MAX_CMAXA_DUE', 'AGR9_MAX_CMAXC_DUE', 'AGR3_MAX_CMAXI_DAYS'] ">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'css' && grupa === 'AGR'">
              <option
                v-for="variable in ['AGR12_MEAN_CMAXC_DUE','AGR9_MEAN_CMAXC_DUE','AGR6_MEAN_CMAXC_DUE','AGR12_MEAN_CMAXA_DUE', 'AGR9_MEAN_CMAXA_DUE']">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'ins' && grupa === 'AGR'">
              <option
                v-for="variable in ['AGR9_MIN_CMAXI_DAYS','AGR9_MIN_CMAXC_DUE','AGR12_MIN_CMAXC_DUE','AGR6_MIN_CMAXC_DUE','AGR9_MEAN_CMAXI_DAYS']">
                {{variable}}
              </option>
            </select>

            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'all' && grupa === 'AGS'">
              <option
                v-for="variable in ['AGS6_MAX_CMAXA_DAYS','AGS9_MAX_CMAXA_DAYS','AGS12_MAX_CMAXA_DAYS','AGS3_MAX_CMAXA_DAYS','AGS6_MAX_CMAXC_DAYS'] ">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'css' && grupa === 'AGS'">
              <option
                v-for="variable in ['AGS9_MEAN_CMAXC_DUE','AGS12_MEAN_CMAXC_DUE','AGS6_MEAN_CMAXC_DUE','AGS6_MAX_CMAXC_DUE','AGS3_MAX_CMAXC_DUE']">
                {{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'ins' && grupa === 'AGS'">
              <option
                v-for="variable in ['AGS3_MAX_CMAXI_DAYS', 'AGS6_MAX_CMAXI_DAYS','AGS9_MAX_CMAXI_DAYS','AGS12_MAX_CMAXI_DAYS','AGS3_MEAN_CMAXI_DAYS']">
                {{variable}}
              </option>
            </select>

            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'all' && grupa === 'APP'">
              <option  v-for="variable in ['APP_CHAR_BRANCH', 'APP_LOAN_AMOUNT', 'APP_N_INSTALLMENTS', 'APP_INSTALLMENT', 'APP_CHAR_JOB_CODE'] ">{{variable}}
              </option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'css' && grupa === 'APP'">
              <option  v-for="variable in ['APP_CHAR_GENDER','APP_CHAR_CARS', 'APP_CHAR_CITY','APP_CHAR_HOME_STATUS','APP_SPENDINGS']">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '1' && walletType === 'ins' && grupa === 'APP'">
              <option  v-for="variable in ['APP_LOAN_AMOUNT', 'APP_N_INSTALLMENTS', 'APP_INSTALLMENT', 'APP_CHAR_CARS', 'APP_SPENDINGS']">{{variable}}</option>
            </select>

            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '2' && walletType === 'all' && grupa === 'ACT'">
              <option  v-for="variable in ['ACT9_N_GOOD_DAYS', 'ACT_CCSS_N_LOAN', 'ACT6_N_GOOD_DAYS', 'ACT_CALL_N_LOAN', 'ACT12_N_GOOD_DAYS'] ">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '2' && walletType === 'css' && grupa === 'ACT'">
              <option  v-for="variable in ['ACT_CCSS_MIN_SENIORITY', 'ACT_CCSS_N_STATB', 'ACT_CCSS_DUEUTL', 'ACT_CCSS_MIN_LNINST', 'ACT9_N_GOOD_DAYS']">{{variable}}</option>
            </select>
            <select class="form-control btn btn-secondary"
                    v-model="variableName"
                    v-if="due === '2' && walletType === 'ins' && grupa === 'ACT'">
              <option  v-for="variable in ['ACT_CALL_CC', 'ACT_LOANINC', 'ACT_CC', 'ACT_CINS_N_STATB', 'ACT_CINS_ALL']">{{variable}}</option>
            </select>
          </div>
        </div>

        <div class="results" v-if="allValuesProvided">
          <h4>Wartości dla klasy: {{ this.getCategories(this.due, this.walletType, this.grupa, this.variableName, 1).war
            }}</h4><br>
          <img
            v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.grupa, this.getGinni(this.due, this.walletType, this.grupa, this.variableName), 1)"
            alt=""/>
          <br>
          <h4>Wartości dla klasy: {{ this.getCategories(this.due, this.walletType, this.grupa, this.variableName, 2).war
            }}</h4><br>
          <img
            v-bind:src="this.getImgUrl(this.host, this.due, this.walletType, this.grupa, this.getGinni(this.due, this.walletType, this.grupa, this.variableName), 2)"
            alt=""/>
          <br>
          <h4>Wartości dla klasy: {{ this.getCategories(this.due, this.walletType, this.grupa, this.variableName, 3).war
            }}</h4>
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

      host: 'https://s3.amazonaws.com/projektsas/projekt_all/',
      due: '1',
      walletType: 'all',
      grupa: 'ACT',
      variableName: 'ACT6_N_GOOD_DAYS',
      bestVariables: {
        ACT: [
          'A'
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

    getACT (due, prod) {
      console.log('PROD: ' + prod)
      return variablesArr.find(x => x.dueOrVin === due && x.prod === prod && x.grupa === 'ACT' && x.kolejnosc_wg_gini === 1).zmienna.toString()
    },
    getImgUrl (host, due, wallet, category, variable, classification) {
      return (host + due + '/' + wallet + '/' + category + '/' + variable + '/' + classification + '/Vin.png').toString()
    },

    getCategories (due1, walletType1, grupa1, zmienna1, klasa1) {
      if (categoriesArr.find(x => x.due === Number(due1) && x.walletType === walletType1 && x.grupa === grupa1 && x.zmienna === zmienna1 && x.klasa === klasa1) === undefined) {
        return 'und'
      } else {
        return categoriesArr.find(x => x.due === Number(due1) && x.walletType === walletType1 && x.grupa === grupa1 && x.zmienna === zmienna1 && x.klasa === klasa1)
      }
    },

    getGinni (due1, product1, grupa1, zmienna1) {
      if (variablesArr.find(x => x.dueOrVin === Number(due1) && x.prod === product1 && x.grupa === grupa1 && x.zmienna === zmienna1) === undefined) {
        return ''
      } else {
        return variablesArr.find(x => x.dueOrVin === Number(due1) && x.prod === product1 && x.grupa === grupa1 && x.zmienna === zmienna1).kolejnosc_wg_gini
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
