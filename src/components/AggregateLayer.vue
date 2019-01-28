<template>
  <div><h4 class="col-lg-8">{{aggregateLayerText}}</h4></div>
</template>

<script>
export default {
  name: 'aggregate-layer',
  data () {
    return {
      aggregateLayerText: 'Warstwa zbiorcza dotyczy analizy vintage kwotowego i ilościowego dla vin=1, 2 oraz 3, ' +
        'a także z podziałem na kredyty gotówkowe i ratalne.'
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
