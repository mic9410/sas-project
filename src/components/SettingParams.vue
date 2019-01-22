<template>
  <div>Zbiorcza - wykresy które pokazują ogólną sytuację - prosty i asymptotyczny, dziedziną są wszystkie obserwacje.
    <br>
    <div class="container select-params">
      <form>
        <div class="form-group row">
          <label for="due" class="col-md-5 col-form-label">Określ due (minimalna liczba opóźnionych rat) </label>
          <select class="form-control col-md-1" id="due">
            <option>1</option>
            <option>2</option>
            <option selected>3</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="wallet-type" class="col-md-5 col-form-label">Typ protfela (kredyt gotówkowy czy raty
            produktu) </label>
          <select class="form-control col-md-1" id="wallet-type">
            <option>all</option>
            <option>css</option>
            <option selected>ins</option>
          </select>
        </div>
        <div class="form-group row">
          <label for="variable-category-type" class="col-md-5 col-form-label">Typ portfela (kredyt gotówkowy czy raty
            produktu)
            <a v-b-tooltip.hover="'ACT - w momencie pomiaru\n' +
            'AGR - kategorie zmiennych behawioralnych, gdzie missing w danych powoduje missing agregatu\n'+
            'APP - opisują klienta w momencie aplikacji\n'+
            'AGS - kategorie zmiennych behawioralnych'"
               variant="outline-success">
              <i class="fas fa-info-circle"></i>
            </a>
          </label>
          <select class="form-control col-md-1" id="variable-category-type">
            <option selected>ACT</option>
            <option>AGR</option>
            <option>APP</option>
            <option>AGS</option>
          </select>
        </div>
        <div class="form-group row">
          <div>
            <ul>
              <li v-for="user in users">
                {{user.firstname}} {{user.lastname}}
              </li>
            </ul>
          </div>
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
      users: [
        {firstname: 'Sebastian', lastname: 'Eschweiler'},
        {firstname: 'Bill', lastname: 'Smith'},
        {firstname: 'John', lastname: 'Porter'}
      ]
    }
  }
}
</script>

<style scoped>
  .select-params {
    background: aliceblue;
  }
</style>
