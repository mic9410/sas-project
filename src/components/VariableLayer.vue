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
        {{this.fileName.toLowerCase()}}
      </form>
      <div class="row align-items-center justify-content-center">
        <button v-on:click="displayResults" class="btn btn-lg btn-info showGraph">Pokaż wykres</button>
      </div>
      <div class="form-group row" v-if="allValuesProvided">
        <img src="D:\Repos\sas-raport\graphs1_all_act_act_age.jpg">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'variable-layer',
  data () {
    return {
      bestVariables: {
        ACT: [
          'act_age',
          'act_cc',
          'act_loaninc',
          'act_call_cc',
          'act_cins_n_loan'],
        AGR: [
          'agr3_Mean_CMaxA_Days',
          'agr3_Mean_CMaxA_Due',
          'agr6_Mean_CMaxI_Days',
          'agr6_Max_CMaxI_Days',
          'agr6_Max_CMaxC_Days'
        ],
        APP: [
          'app1',
          'app2',
          'app3',
          'app4',
          'app5'
        ],
        AGS: [
          'ags12_Max_CMaxC_Due',
          'ags12_Mean_CMaxC_Due',
          'ags9_Mean_CMaxA_Days',
          'ags9_Mean_CMaxC_Days',
          'ags6_Mean_CMaxA_Days'
        ]
      },
      due: '',
      walletType: '',
      categoryType: '',
      variableName: '',
      fileName: '',
      variableLayerText: 'W warstwie zmiennych przyjrzmy się bliżej, jaki wpływ na ostateczny rezultat mają pojedyncze zmienne. ' +
      'Z każdej kategorii wybieramy pięć najlepszych na podstawie wartości współczynnika Ginie\'go.'
    }
  },
  methods: {
    displayResults: function (event) {
      // `this` inside methods points to the Vue instance
      // `event` is the native DOM event
      if (event && this.allValuesProvided()) {
        this.fileName = 'D:\\Repos\\sas-raport\\graphs' + this.due + '_' + this.walletType + '_' + this.categoryType + '_' + this.variableName + '.jpg'
      } else {
        alert('Nie można wygenerować wykresu.\n' +
            'Upewnij sie, że uzupełniłeś wszystkie pola.')
      }
    },

    allValuesProvided: function () {
      return this.due !== '' &&
          this.walletType !== '' &&
          this.categoryType !== '' &&
          this.variableName !== ''
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

  label {
    text-align-all: left;
  }
</style>
