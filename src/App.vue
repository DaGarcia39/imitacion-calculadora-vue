<template>
  <div id="app" class="container bg-dark">
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator,
  }
}
</script>

<style lang="scss">
  @import './styles/stylesApp.scss';
</style>
