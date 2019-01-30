<template>
  <div id="app">
    <!--<Calculator></Calculator>
    <hr>-->
    <Calculator2></Calculator2>
  </div>
</template>

<script>
import Calculator from './components/Calculator'
import Calculator2 from './components/Calculator2'

export default {
  name: 'app',
  components: {
    Calculator, Calculator2
  }
}
</script>

<style>
.row {
  text-align: right;
}
.col-3 {
  text-align: center;
}
.col-6 {
  text-align: center;
}
</style>
