<template>
  <div>Zbiorcza - wykresy które pokazują ogólną sytuację - prosty i asymptotyczny, dziedziną są wszystkie obserwacje.
    <br>
    <div class="container select-params">
      <form>
        <div class="form-group row">
          <label for="due" class="col-md-5 col-form-label">Określ due (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-1" id="due" v-model="due">
            <option>1</option>
            <option>2</option>
            <option selected>3</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-type" class="col-md-5 col-form-label">Typ protfela (kredyt gotówkowy czy raty
            produktu) </label>
          <select class="form-control col-md-1" id="wallet-type" v-model="walletType">
            <option>all</option>
            <option>css</option>
            <option selected>ins</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="variable-category-type" class="col-md-5 col-form-label">Kategoria zmiennej
            <a v-b-tooltip.hover="'ACT - w momencie pomiaru\n' +
            'AGR - kategorie zmiennych behawioralnych, gdzie missing w danych powoduje missing agregatu\n'+
            'APP - opisują klienta w momencie aplikacji\n'+
            'AGS - kategorie zmiennych behawioralnych'"
               variant="outline-success">
              <i class="fas fa-info-circle"></i>
            </a>
          </label>
          <select class="form-control col-md-1" id="variable-category-type" v-model="categoryType">
            <option>ACT</option>
            <option>AGR</option>
            <option>APP</option>
            <option>AGS</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-type" class="col-md-5 col-form-label">Wybierz jedną z top 5 najistotniejszych
            zmiennych</label>
          <div id="variableName">
            <select class="form-control"
                    v-model="variableName"
                    v-if="categoryType === 'ACT'">
              <option v-for="variable in bestVariables.ACT">{{variable}}</option>
            </select>
            <select class="form-control"
                    v-model="variableName"
                    v-if="categoryType === 'AGR'">
              <option v-for="variable in bestVariables.AGR">{{variable}}</option>
            </select>
            <select class="form-control"
                    v-model="variableName"
                    v-if="categoryType === 'APP'">
              <option v-for="variable in bestVariables.APP">{{variable}}</option>
            </select>
            <select class="form-control"
                    v-model="variableName"
                    v-if="categoryType === 'AGS'">
              <option v-for="variable in bestVariables.AGS">{{variable}}</option>
            </select>
          </div>
        </div>
        <div class="form-group row">
          <button v-on:click="displayResults">Pokaż wykres</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  name: 'setting-params',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
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
      graphPath: ''
    }
  },
  methods: {
    displayResults: function (event) {
      // `this` inside methods points to the Vue instance
      // `event` is the native DOM event
      if (event && this.allValuesProvided()) {
        this.fileName = this.due + '_' + this.walletType + '_' + this.categoryType + '_' + this.variableName + '.jpg'
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
  .select-params {
    background: aliceblue;
  }
</style>
