<template>
  <calculator>
  </calculator>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'app',
  components: {
    Calculator
  }
}
</script>

<style>
body {
  background-color: rgba(255, 255, 255, 0.733);
  background-image: url('~@/assets/bgCalc.jpg');
  background-blend-mode: color;
}
</style>