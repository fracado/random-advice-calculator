<template>
  <div class="container">
    <div class="calculator">



    </div>
  </div>
</template>

<script>
export default {
  name: 'Simple Vue Calculator',
  data(){
    return {
      calculator: {
        previous: null,
        current: '',
        operator: null,
        operatorClicked: false,
        sign: '',
        end: false
      }
    }
  }
  
}
</script>

<!-- CSS STYLING -->
<style scoped>

</style>
