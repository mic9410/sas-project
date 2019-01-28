<template>
  <div>
    <introduction></introduction><br>
    <setting-params></setting-params><br>
    <variable-layer></variable-layer><br>
  </div>
</template>

<script>
import VariableLayer from './VariableLayer'
import Introduction from './Introduction'
import SettingParams from './SettingParams'

export default {
  components: {
    Introduction,
    VariableLayer,
    SettingParams
  },
  name: 'Index',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
