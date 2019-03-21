<template>
  <div class="container">
    <div class="calculator">
      <!-- SHOW PREVIOUS INPUT -->
      <div class="prev">{{ calculator.previous || '' }} {{ calculator.sign }}</div>
      <!-- SHOW INPUT DISPLAY -->
      <div class="display">{{ calculator.current || '0' }}</div>
      <!-- SHOW CLICKABLE BUTTONS -->
      <div @click="clearAll" class="btn operator2 c">C</div>
      <div @click="del" class="btn operator2">←</div>
      <div @click="divide" class="btn operator2">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="times" class="btn operator2">x</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="minus" class="btn operator2">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn operator2">+</div>
      <div @click="sign" class="btn">±</div>
      <div @click="append('0')" class="btn">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator2">=</div>

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

.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(30px, auto);
  text-align: center;
  width: 250px;
  height: 450px;
}

.display {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  grid-column:  1 / 5;
}

.prev {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  grid-column:  1 / 5;
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #333;
}

.c {
  grid-column:  1 / 3;
}

</style>
