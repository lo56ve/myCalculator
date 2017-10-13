<template>
  <div class="calculator-wrapper">
    <div class="calculator-inner">
      <div class="calculator-display">
        <div class="calculator-formula">{{ formula }}</div>
        <div class="calculator-result">{{ result }}</div>
      </div>
      <div class="calculator-keys">
        <div class="calculator-item1">
          <span @click="backspace">←</span>
          <span @click="cleanFormula">CE</span>
          <span @click="clearAll">C</span>
          <span @click="minus">±</span>
          <span @click="sqrt">√</span>
        </div>
        <div class="calculator-item2">
          <span @click="addString(7)">7</span>
          <span @click="addString(8)">8</span>
          <span @click="addString(9)">9</span>
          <span @click="addString('/')">/</span>
          <span @click="addString('%')">%</span>
        </div>
        <div class="calculator-item3">
          <span @click="addString(4)">4</span>
          <span @click="addString(5)">5</span>
          <span @click="addString(6)">6</span>
          <span @click="addString('*')">*</span>
          <span @click="reciprocal">1/x</span>
        </div>
        <div class="calculator-item4">
          <span @click="addString(1)">1</span>
          <span @click="addString(2)">2</span>
          <span @click="addString(3)">3</span>
          <span @click="addString('-')">-</span>
          <span @click="addString('+')">+</span>
        </div>
        <div class="calculator-item5">
          <span @click="addString(0)">0</span>
          <span @click="addString('.')">.</span>
          <span @click="calcu">=</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        formula: '',
        result: '0'
      }
    },
    methods: {
      backspace () {
        this.formula = this.formula.slice(0, this.formula.length - 1)
      },
      clearAll () {
        this.formula = ''
        this.result = '0'
      },
      addString (a) {
        this.formula += a
      },
      calcu () {
        this.result = eval(this.formula)  // eslint-disable-line
      },
      sqrt () {
        this.result = Math.sqrt(this.formula)
      },
      minus () {
        if (this.formula.length > 0) {
          this.calcu()
          this.formula = this.formula.indexOf('-(') < 0 ? `-(${this.formula})` : this.formula.slice(2, -1)
          this.result = this.result.toString().indexOf('-') < 0 ? '-' + this.result : this.result.toString().slice(1)
        }
      },
      reciprocal () {
        if (this.formula.length > 0) {
          this.formula = this.formula.indexOf('1/(') < 0 ? `1/(${this.formula})` : this.formula.slice(3, -1)
          this.calcu()
        }
      },
      cleanFormula () {
        this.formula = ''
      }
    }
  }
</script>

<style>
  .calculator-wrapper {
    border-radius: 13px;
    background-color: gray;
    padding: 10px;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.2);
    display: inline-block;
    margin-bottom: 40px;
  }
  .calculator-inner {
    background-color: darkcyan;
    padding: 10px 10px 40px 10px;
  }
  .calculator-display {
    padding: 8px 13px 5px 13px;
    width: 380px;
    font-size: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid rgb(185, 180, 180);
    text-align: right;
    box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.2);
    margin-bottom: 35px;
  }
  .calculator-formula {
    margin-bottom: 20px;
    height: 23px;
  }
  .calculator-keys span {
    font-size: 18px;
    width: 67px;
    height: 50px;
    display: inline-block;
    line-height: 50px;
    margin: 8px 10px 0 0;
    border: 1px solid rgba(0, 0, 0, 0.5);
    border-radius: 8px;
    box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.5);
  }
  .calculator-keys span:hover {
    color: white;
    box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.2);
    cursor: pointer;
  }
  .calculator-item5 span:first-child,.calculator-item5 span:last-child {
    width:150px;
  }

</style>