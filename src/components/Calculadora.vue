<template>
  <div class="calculadora">
    <div class="display">{{ valueCurrent || '0' }}</div>
    <div @click="clear" class="button">C</div>
    <div @click="signal" class="button">+/-</div>
    <div @click="porcent" class="button">%</div>
    <div @click="divide" class="button operator">÷</div>
    <div @click="join('7')" class="button">7</div>
    <div @click="join('8')" class="button">8</div>
    <div @click="join('9')" class="button">9</div>
    <div @click="mult" class="button operator">x</div>
    <div @click="join('4')" class="button">4</div>
    <div @click="join('5')" class="button">5</div>
    <div @click="join('6')" class="button">6</div>
    <div @click="sub" class="button operator">-</div>
    <div @click="join('1')" class="button">1</div>
    <div @click="join('2')" class="button">2</div>
    <div @click="join('3')" class="button">3</div>
    <div @click="add" class="button operator">+</div>
    <div @click="join('0')" class="button zero">0</div>
    <div @click="point" class="button">.</div>
    <div @click="res" class="button">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valueCurrent: '',
      valueAfter: null,
      operator: null,
      clickOperator: false,
    }
  },
  methods: {
    clear() {
      this.valueCurrent = ''
    },
    join(number) {
      if(this.clickOperator) {
        this.valueCurrent = '';
        this.clickOperator = false;
      }
      this.valueCurrent = `${this.valueCurrent}${number}`;
    },
    point() {
      if(this.valueCurrent.indexOf('.') == -1) {
        this.join('.');
      }
    },
    setValue() {
      this.valueAfter = this.valueCurrent;
      this.clickOperator = true;
    },
    signal() {
      this.valueCurrent = this.valueCurrent.charAt(0) == '-'
      ? this.valueCurrent.slice(1)
      : `-${this.valueCurrent}`
    },
    porcent() {
      this.valueCurrent = `${parseFloat(this.valueCurrent)/ 100}`
    },
    divide() {
      this.operator = (val1, val2) => val1 / val2;
      this.setValue();
    },
    mult() {
      this.operator = (val1, val2) => val1 * val2;
      this.setValue();
    },
    add() {
      this.operator = (val1, val2) => val1 + val2;
      this.setValue();
    },
    sub() {
      this.operator = (val1, val2) => val1 - val2;
      this.setValue();
    },
    res() {
      this.valueCurrent = `${this.operator(
        parseFloat(this.valueAfter),
        parseFloat(this.valueCurrent),
      )}`;
      this.valueAfter = null;
    }
  }
};
</script>

<style scoped>
.calculadora {
  margin: 0 auto;
  width: 350px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.button {
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
</style>