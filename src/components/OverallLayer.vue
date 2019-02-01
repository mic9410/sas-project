<template>
  <div>
    <div><h4 id="test-anchor" class="col-lg-8">{{this.aggregatedLayerText}}</h4></div>
    <div class="container select-params col-md-8 align-content-center">
      <form>
        <div class="form-group row">
          <label for="dueOL" class="col-md-6 col-form-label">Określ vin (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-2 btn btn-secondary " id="dueOL" v-model="dueOL">
            <option selected>1</option>
            <option>2</option>
            <option>3</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-typeOL" class="col-md-6 col-form-label">Typ protfela (kredyt gotówkowy czy raty
            produktu) </label>
          <select class="form-control col-md-2 btn btn-secondary" id="wallet-typeOL" v-model="walletTypeOL">
            <option selected>all</option>
            <option>css</option>
            <option>ins</option>
          </select>
        </div>
      </form>
      <div class="results" v-if="allValuesProvidedOL">
        <template>
          <b-table v-if="this.dueOL === '1' && this.walletTypeOL === 'all'" striped hover :items="items.all_1"></b-table>
          <b-table v-if="this.dueOL === '2' && this.walletTypeOL === 'all'" striped hover :items="items.all_2"></b-table>
          <b-table v-if="this.dueOL === '3' && this.walletTypeOL === 'all'" striped hover :items="items.all_3"></b-table>
          <b-table v-if="this.dueOL === '1' && this.walletTypeOL === 'css'" striped hover :items="items.css_1"></b-table>
          <b-table v-if="this.dueOL === '2' && this.walletTypeOL === 'css'" striped hover :items="items.css_2"></b-table>
          <b-table v-if="this.dueOL === '3' && this.walletTypeOL === 'css'" striped hover :items="items.css_3"></b-table>
          <b-table v-if="this.dueOL === '1' && this.walletTypeOL === 'ins'" striped hover :items="items.ins_1"></b-table>
          <b-table v-if="this.dueOL === '2' && this.walletTypeOL === 'ins'" striped hover :items="items.ins_2"></b-table>
          <b-table v-if="this.dueOL === '3' && this.walletTypeOL === 'ins'" striped hover :items="items.ins_3"></b-table>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
const items = {
  all_1: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CCSS_N_LOAN',
      '#2': 'ACT_CALL_N_LOAN',
      '#3': 'ACT3_N_GOOD_DAYS',
      '#4': 'ACT6_N_GOOD_DAYS',
      '#5': 'ACT9_N_GOOD_DAYS'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR6_MAX_CMAXA_DAYS',
      '#2': 'AGR6_MAX_CMAXC_DAYS',
      '#3': 'AGR6_MAX_CMAXA_DUE',
      '#4': 'AGR9_MAX_CMAXC_DUE',
      '#5': 'AGR3_MAX_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS6_MAX_CMAXA_DAYS',
      '#2': 'AGS9_MAX_CMAXA_DAYS',
      '#3': 'AGS12_MAX_CMAXA_DAYS',
      '#4': 'AGS3_MAX_CMAXA_DAYS',
      '#5': 'AGS6_MAX_CMAXC_DAYS'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_CHAR_BRANCH',
      '#2': 'APP_LOAN_AMOUNT',
      '#3': 'APP_N_INSTALLMENTS',
      '#4': 'APP_INSTALLMENT',
      '#5': 'APP_CHAR_JOB_CODE'
    }
  ],
  all_2: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT9_N_GOOD_DAYS',
      '#2': 'ACT_CCSS_N_LOAN',
      '#3': 'ACT6_N_GOOD_DAYS',
      '#4': 'ACT_CALL_N_LOAN',
      '#5': 'ACT12_N_GOOD_DAYS'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR3_MEAN_CMAXI_DAYS',
      '#2': 'AGR3_MAX_CMAXI_DAYS',
      '#3': 'AGR12_MAX_CMAXA_DUE',
      '#4': 'AGR9_MAX_CMAXA_DUE',
      '#5': 'AGR6_MAX_CMAXA_DUE'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS9_MAX_CMAXA_DAYS',
      '#2': 'AGS12_MAX_CMAXA_DAYS',
      '#3': 'AGS12_MEAN_CMAXI_DAYS',
      '#4': 'AGS12_MAX_CMAXI_DAYS',
      '#5': 'AGS9_MAX_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_CHAR_BRANCH',
      '#2': 'APP_LOAN_AMOUNT',
      '#3': 'APP_INSTALLMENT',
      '#4': 'APP_N_INSTALLMENTS',
      '#5': 'APP_CHAR_CARS'
    }
  ],
  all_3: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT3_N_GOOD_DAYS',
      '#2': 'ACT6_N_GOOD_DAYS',
      '#3': 'ACT_CCSS_N_LOAN',
      '#4': 'ACT_CALL_N_LOAN',
      '#5': 'ACT9_N_GOOD_DAYS'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR3_MIN_CMAXI_DAYS',
      '#2': 'AGR3_MAX_CMAXI_DAYS',
      '#3': 'AGR6_MAX_CMAXA_DUE',
      '#4': 'AGR6_MIN_CMAXI_DAYS',
      '#5': 'AGR3_MEAN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS9_MAX_CMAXA_DAYS',
      '#2': 'AGS12_MAX_CMAXA_DAYS',
      '#3': 'AGS12_MIN_CMAXI_DAYS',
      '#4': 'AGS12_MAX_CMAXI_DAYS',
      '#5': 'AGS9_MIN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_CHAR_BRANCH',
      '#2': 'APP_LOAN_AMOUNT',
      '#3': 'APP_INSTALLMENT',
      '#4': 'APP_N_INSTALLMENTS',
      '#5': 'APP_CHAR_CARS'
    }
  ],
  css_1: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CCSS_N_STATB',
      '#2': 'ACT_CCSS_MIN_LNINST',
      '#3': 'ACT_CCSS_MIN_PNINST',
      '#4': 'ACT9_N_GOOD_DAYS',
      '#5': 'ACT12_N_GOOD_DAYS'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR12_MEAN_CMAXC_DUE',
      '#2': 'AGR9_MEAN_CMAXC_DUE',
      '#3': 'AGR6_MEAN_CMAXC_DUE',
      '#4': 'AGR12_MEAN_CMAXA_DUE',
      '#5': 'AGR9_MEAN_CMAXA_DUE'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS9_MEAN_CMAXC_DUE',
      '#2': 'AGS12_MEAN_CMAXC_DUE',
      '#3': 'AGS6_MEAN_CMAXC_DUE',
      '#4': 'AGS6_MAX_CMAXC_DUE',
      '#5': 'AGS3_MAX_CMAXC_DUE'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_CHAR_GENDER',
      '#2': 'APP_CHAR_CARS',
      '#3': 'APP_CHAR_CITY',
      '#4': 'APP_CHAR_HOME_STATUS',
      '#5': 'APP_SPENDINGS'
    }
  ],
  css_2: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CCSS_MIN_SENIORITY',
      '#2': 'ACT_CCSS_N_STATB',
      '#3': 'ACT_CCSS_DUEUTL',
      '#4': 'ACT_CCSS_MIN_LNINST',
      '#5': 'ACT9_N_GOOD_DAYS'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR12_MEAN_CMAXC_DUE',
      '#2': 'AGR12_MAX_CMAXC_DUE',
      '#3': 'AGR9_MAX_CMAXC_DUE',
      '#4': 'AGR12_MAX_CMAXC_DAYS',
      '#5': 'AGR6_MAX_CMAXC_DUE'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS12_MEAN_CMAXC_DUE',
      '#2': 'AGS12_MAX_CMAXC_DUE',
      '#3': 'AGS6_MAX_CMAXC_DUE',
      '#4': 'AGS9_MAX_CMAXC_DUE',
      '#5': 'AGS9_MEAN_CMAXC_DUE'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_CHAR_GENDER',
      '#2': 'APP_CHAR_CITY',
      '#3': 'APP_CHAR_CARS',
      '#4': 'APP_CHAR_HOME_STATUS',
      '#5': 'APP_SPENDINGS'
    }
  ],
  css_3: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CCSS_MIN_SENIORITY',
      '#2': 'ACT_CCSS_N_STATB',
      '#3': 'ACT_CCSS_DUEUTL',
      '#4': 'ACT_CCSS_MAXDUE',
      '#5': 'ACT_CMAXC_DUE'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR6_MEAN_CMAXC_DUE',
      '#2': 'AGR12_MEAN_CMAXC_DUE',
      '#3': 'AGR12_MAX_CMAXC_DUE',
      '#4': 'AGR12_MAX_CMAXC_DAYS',
      '#5': 'AGR9_MAX_CMAXC_DUE'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS6_MEAN_CMAXC_DUE',
      '#2': 'AGS12_MEAN_CMAXC_DUE',
      '#3': 'AGS6_MAX_CMAXC_DUE',
      '#4': 'AGS9_MAX_CMAXC_DUE',
      '#5': 'AGS12_MAX_CMAXC_DUE'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_CHAR_GENDER',
      '#2': 'APP_CHAR_CITY',
      '#3': 'APP_CHAR_HOME_STATUS',
      '#4': 'APP_CHAR_CARS',
      '#5': 'APP_NUMBER_OF_CHILDREN'
    }
  ],
  ins_1: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CINS_N_STATB',
      '#2': 'ACT_CALL_ALL',
      '#3': 'ACT_CINS_ACP',
      '#4': 'ACT_LOANINC',
      '#5': 'ACT_CC'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR9_MIN_CMAXI_DAYS',
      '#2': 'AGR9_MIN_CMAXC_DUE',
      '#3': 'AGR12_MIN_CMAXC_DUE',
      '#4': 'AGR6_MIN_CMAXC_DUE',
      '#5': 'AGR9_MEAN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS3_MAX_CMAXI_DAYS',
      '#2': 'AGS6_MAX_CMAXI_DAYS',
      '#3': 'AGS9_MAX_CMAXI_DAYS',
      '#4': 'AGS12_MAX_CMAXI_DAYS',
      '#5': 'AGS3_MEAN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_LOAN_AMOUNT',
      '#2': 'APP_N_INSTALLMENTS',
      '#3': 'APP_INSTALLMENT',
      '#4': 'APP_CHAR_CARS',
      '#5': 'APP_SPENDINGS'
    }
  ],
  ins_2: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CALL_CC',
      '#2': 'ACT_LOANINC',
      '#3': 'ACT_CC',
      '#4': 'ACT_CINS_N_STATB',
      '#5': 'ACT_CINS_ALL'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR3_MAX_CMAXI_DAYS',
      '#2': 'AGR6_MIN_CMAXI_DAYS',
      '#3': 'AGR6_MAX_CMAXI_DAYS',
      '#4': 'AGR9_MIN_CMAXI_DAYS',
      '#5': 'AGR12_MIN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS9_MEAN_CMAXI_DAYS',
      '#2': 'AGS3_MAX_CMAXI_DAYS',
      '#3': 'AGS6_MAX_CMAXI_DAYS',
      '#4': 'AGS9_MAX_CMAXI_DAYS',
      '#5': 'AGS3_MEAN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_LOAN_AMOUNT',
      '#2': 'APP_INSTALLMENT',
      '#3': 'APP_N_INSTALLMENTS',
      '#4': 'APP_CHAR_CARS',
      '#5': 'APP_CHAR_GENDER'
    }
  ],
  ins_3: [
    {
      KategoriaZmiennej: 'ACT',
      '#1': 'ACT_CALL_CC',
      '#2': 'ACT_CC',
      '#3': 'ACT_LOANINC',
      '#4': 'ACT_CINS_N_STATB',
      '#5': 'ACT_CINS_ACP'
    },
    {
      KategoriaZmiennej: 'AGR',
      '#1': 'AGR3_MIN_CMAXI_DAYS',
      '#2': 'AGR6_MIN_CMAXI_DAYS',
      '#3': 'AGR3_MEAN_CMAXI_DAYS',
      '#4': 'AGR6_MAX_CMAXI_DAYS',
      '#5': 'AGR9_MIN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'AGS',
      '#1': 'AGS9_MEAN_CMAXI_DAYS',
      '#2': 'AGS6_MIN_CMAXI_DAYS',
      '#3': 'AGS6_MAX_CMAXI_DAYS',
      '#4': 'AGS12_MEAN_CMAXI_DAYS',
      '#5': 'AGS6_MEAN_CMAXI_DAYS'
    },
    {
      KategoriaZmiennej: 'APP',
      '#1': 'APP_LOAN_AMOUNT',
      '#2': 'APP_INSTALLMENT',
      '#3': 'APP_N_INSTALLMENTS',
      '#4': 'APP_CHAR_MARITAL_STATUS',
      '#5': 'APP_CHAR_CARS'
    }
  ]
}

export default {
  name: 'overall-layer',
  data () {
    return {
      items: items,
      hostOL: 'https://s3.amazonaws.com/projektsas/projekt_all/',
      dueOL: '1',
      walletTypeOL: 'all',
      aggregatedLayerText: 'W warstwie identyfikacji zmiennych przedstawimy po 5 zmiennych o najwyższym współczynniku Giniego, zaczynając od najistotniejszych. ' +
        'Zawartość tabeli jak i kolejność jest różna ,w zależności od zdefiniowanego Vin oraz typu portfela.'
    }
  },
  methods: {
    allValuesProvidedOL: function () {
      return this.dueOL !== '' &&
          this.walletTypeOL !== ''
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
