<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <button @click="clear" class="button">C</button>
    <button @click="sign" class="button">+/-</button>
    <button @click="percent" class="button">%</button>
    <button @click="divide" class="button operator">÷</button>
    <button @click="append('7')" class="button">7</button>
    <button @click="append('8')" class="button">8</button>
    <button @click="append('9')" class="button">9</button>
    <button @click="times" class="button operator">x</button>
    <button @click="append('4')" class="button">4</button>
    <button @click="append('5')" class="button">5</button>
    <button @click="append('6')" class="button">6</button>
    <button @click="minus" class="button operator">-</button>
    <button @click="append('1')" class="button">1</button>
    <button @click="append('2')" class="button">2</button>
    <button @click="append('3')" class="button">3</button>
    <button @click="add" class="button operator">+</button>
    <button @click="append('0')" class="button zero">0</button>
    <button @click="dot" class="button">.</button>
    <button @click="equal" class="button operator">=</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
          this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
      )}`;
      this.previous = '';
    }
  }
}
</script>

<style scoped>
.calculator {
  width: 800px;
  margin: 0 auto;
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
  position: center;
}

.button {
  background-color: #F2F2F2;
  border: none;
  font-size: 40px;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
