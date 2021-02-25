<template>
  <div class="container p-3">
    <div class="calculator p-3">
      <div class="display"><input type="number" class="form-control" placeholder="0" v-model="result"></div>

      <div class="clear"><b-button block variant="danger" @click="clear">C</b-button></div>
      <div><b-button block variant="warning" @click="changeSign">+/-</b-button></div>
      <div><b-button block variant="warning" @click="porcent">%</b-button></div>

      <div v-for="item in thirdPart" :key="item"><b-button block variant="info" @click="addNumber(item)">{{ item }}</b-button></div>
      <div><b-button block variant="primary" @click="getOperator('/')">/</b-button></div>

      <div v-for="item in secondPart" :key="item"><b-button block variant="info" @click="addNumber(item)">{{ item }}</b-button></div>
      <div><b-button block variant="primary" @click="getOperator('*')">X</b-button></div>

      <div v-for="item in firtsPart" :key="item"><b-button block variant="info" @click="addNumber(item)">{{ item }}</b-button></div>
      <div><b-button block variant="primary" @click="getOperator('-')">-</b-button></div>

      <div class="zero"><b-button block variant="info" @click="addNumber(0)">0</b-button></div>
      <div><b-button block variant="success" @click="equal">=</b-button></div>
      <div><b-button block variant="primary" @click="getOperator('+')">+</b-button></div>
    </div>
    <!-- {{firstNumber}} {{operator}} {{secondNumber}} = {{result}} -->
    <div class="bg-info p-3 historyContainer">
      <History :arrayLoaded="arrayEmpty" :enviarAlert="mostrar" @returnResult="resultInHistory = $event"/>
    </div>
  </div>
</template>

<script>
import History from '@/components/History.vue'

export default {
  name: 'Calculator',
  components: {
    History
  },
  data() {
    return {
      result: 0,
      temporal_value: 0,
      operator: undefined,
      reset: false,
      firstNumber: 0,
      secondNumber: 0,
      value: 0,
      arrayEmpty: [],
      resultInHistory: null,
      firtsPart: [ 1, 2, 3 ],
      secondPart: [ 4, 5, 6 ],
      thirdPart: [ 7, 8, 9 ]
    }
  },
  methods: {
    clear() {
      this.result = 0;
      this.temporal_value = 0;
      this.operator = undefined;
    },
    changeSign() {  
      this.result *= -1;
    },
    porcent() {
      this.result /= 100;
    },
    addNumber(number) {
      if(this.result == 0 || this.reset === true) {
        this.result = '';
        this.reset = false;
      }
      this.result += number.toString();
    },
    getOperator(operator) {
      this.temporal_value = this.result;
      this.operator = operator;
      this.reset = true;
    },
    equal() {
      this.calculate();
      this.temporal_value = 0;
      this.sendInformation()
    },
    calculate() {
      this.value = 0;
      this.firstNumber = parseFloat(this.temporal_value);
      this.secondNumber = parseFloat(this.result);

      switch(this.operator) {
        case '+':
          this.value = this.firstNumber + this.secondNumber;
          break;
        case '-':
          this.value = this.firstNumber - this.secondNumber;
          break;
        case '*':
          this.value = this.firstNumber * this.secondNumber;
          break;
        case '/':
          this.value = this.firstNumber / this.secondNumber;  
      }

    this.result = this.value.toString();  
    },
    sendInformation() {
      this.arrayEmpty.unshift(
        {
          num1: this.firstNumber,
          simbol: this.operator,
          num2: this.secondNumber,
          total: this.result
        }
      );
    },
    mostrar() {
      this.result = this.resultInHistory;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import '../styles/stylesCalculator.scss';
</style>
