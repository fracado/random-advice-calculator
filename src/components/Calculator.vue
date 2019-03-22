<template>
  <div class="container">
    <h1>Random Advice Calculator</h1>
    <div class="calculator">
      <!-- show previous input -->
      <div class="prev">{{ calculator.previous || '' }} {{ calculator.sign }} </div>
      <!-- show current input in display -->
      <div class="display">{{ calculator.current || '0' }}</div>
      <!-- show API info -->
      <div class="info">{{ calculator.info }}</div>
      <!-- show buttons with methods on click -->
      <div @click="clearAll" class="btn operator c">C</div>
      <div @click="del" class="btn operator">←</div>
      <div @click="divide" class="btn operator">/</div>
      <div @click="append('7')" class="btn">7</div>
      <div @click="append('8')" class="btn">8</div>
      <div @click="append('9')" class="btn">9</div>
      <div @click="multiply" class="btn operator">x</div>
      <div @click="append('4')" class="btn">4</div>
      <div @click="append('5')" class="btn">5</div>
      <div @click="append('6')" class="btn">6</div>
      <div @click="substract" class="btn operator">-</div>
      <div @click="append('1')" class="btn">1</div>
      <div @click="append('2')" class="btn">2</div>
      <div @click="append('3')" class="btn">3</div>
      <div @click="add" class="btn operator">+</div>
      <div @click="sign" class="btn">±</div>
      <div @click="append('0')" class="btn">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator">=</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
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
        info: null
      }
    }
  },

  methods: {
    // attaches numbers clicked
    append(number) {
      if (this.calculator.operatorClicked) {
          this.calculator.current = ''
          this.calculator.operatorClicked = false
        }
        this.calculator.current = `${this.calculator.current}${number}`
    },
    // returns result from calculation
    equal() {
      this.calculator.current = this.calculator.operator(
        parseFloat(this.calculator.previous),
        parseFloat(this.calculator.current)
      )
      this.calculator.previous = null
      this.calculator.sign = ''
      this.calculator.operatorClicked = true;     
      axios
      .get('https://api.adviceslip.com/advice')
      .then(response => (this.calculator.info = '"'+ response.data.slip.advice +'"'))
    },
    // basic operators: add, substract, multiply, divide
    add() {
      this.calculator.operator = (a, b) => a + b
      this.setPrevious()
      this.calculator.sign = '+'
    },
    substract() {
      this.calculator.operator = (a, b) => a - b
      this.setPrevious()
      this.calculator.sign = '-'
    },
    multiply() {
      this.calculator.operator = (a, b) => a * b
      this.setPrevious()
      this.calculator.sign = 'x'
    },
    divide() {
      this.calculator.operator = (a, b) => a / b
      this.setPrevious()
      this.calculator.sign = '/'
    },
    // to show previous input
    setPrevious() {
      this.calculator.previous = this.calculator.current
      this.calculator.operatorClicked = true;
    },
    // to change sign in front of number -/+
    sign() {
      if(this.calculator.current != '')
        this.calculator.current = this.calculator.current.charAt(0) === '-' ?
          this.calculator.current.slice(1) : `-${this.calculator.current}`
    },
    // add decimal dot
    dot() {
      if (this.calculator.current.indexOf('.') === -1)
        this.append('.')
    },
    // reset current input
    del() {
      if(this.calculator.current)
        this.calculator.current = this.calculator.current.slice(0, -1)
    },
    // clear input and result   
    clearAll() {
      this.calculator.current = ''
      this.calculator.previous = null
      this.calculator.sign = ''
    },
  },
}
</script>

<!-- CSS STYLING -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Teko');

.container {
  padding-top: 40px;
}

.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(30px, auto);
  text-align: center;
  width: 300px;
  height: 500px;
  margin: 0 auto;
  box-shadow: 4px 3px 2px 0px #c9c8c88c;
  font-family: 'Teko', sans-serif;
  font-size: 30px;
}

.display {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  grid-column:  1 / 5;
  padding: 0 10px 0 0;
  background-color: rgb(226, 225, 225);
  box-shadow: inset 0 0 12px #1f1e1e;
}

.prev {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  grid-column:  1 / 5;
  padding: 0 10px 0 0;
  min-height: 43px;
  background-color: #333;
  color: #fff;
  border: 1px solid #eee
}

.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #333;
  background-color: aliceblue;
}

.c {
  grid-column:  1 / 3;
}

.btn:hover { 
  background-color: rgba(36, 163, 146, 0.575); 
  cursor: pointer; 
}

.operator { 
  background-color:rgb(88, 215, 204) 
}

.operator:hover { 
  background-color: rgba(31, 116, 122, 0.829); 
  cursor: pointer; 
}

.info {
  grid-column:  1 / 5;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid #333;
  font-style: italic;
  padding: 2px;
  background-color: aliceblue;
}

h1 {
  text-align: center;
  font-size: 46px;
  margin-bottom: 2.6rem;
  text-shadow: 1px 2px 5px rgba(125, 125, 125, 0.4);
}

</style>
