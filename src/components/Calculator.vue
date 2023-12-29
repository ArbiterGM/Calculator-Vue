<template>
  <div class="calculator">
    <div class="display">{{ displayValue || 0 }}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="operator" @click="times">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="operator" @click="plus">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="operator" @click="calculate">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      displayValue: "",
      previous: "",
      operatorClicked: false,
      operator: null,
    }
  },
  methods: {
    clear() {
      this.displayValue = "";
      this.operator = "";
      this.previous = "";
    },
    sign() {
      this.displayValue = this.displayValue.charAt(0) === "-" || this.displayValue < 0 ? this.displayValue.slice(1) : `-${this.displayValue}`
    },
    percent() {
      this.displayValue = `${parseFloat(this.displayValue) / 100}`
    },
    append(num) {
      if (this.operatorClicked) {
        this.displayValue = "";
        this.operatorClicked = false;
      }
      this.displayValue = `${this.displayValue}${num}`;
    },
    // დასფიქსია შედეგის მიღების შემდგომ წერტილზე დაწოლით გამოწვეული ერორი
    dot() {
      if (this.displayValue.indexOf(".") === -1) this.append('.');
    },
    setPrevious() {
      this.previous = this.displayValue;
      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    calculate() {
      this.displayValue = `${this.operator(parseFloat(this.previous), parseFloat(this.displayValue))}`;
      this.previous = null;
    },
  }
}
</script>

<style scoped lang="scss">
.calculator {
  overflow: hidden;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  width: 330px;
  font-size: 2rem;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  border-radius: 4px;

  div {
    background-color: #e7e7e7;
    border: 1px solid #363636;
    height: 65px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .btn {
    cursor: pointer;
    min-width: 65px;

    &:hover {
      background-color: #d1d1d1;
      transition: .2s linear;
    }
  }

  .display {
    cursor: default;
    color: white;
    font-size: 2.8rem;
    grid-column: 1 / 5;
    background-color: #345490;
    height: 4.2rem;
    padding-right: 1rem;
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }

  .operator {
    background-color: #ffb835;
    cursor: pointer;

    &:hover {
      background-color: #ffa600;
      transition: .2s linear;
    }
  }

  .zero {
    grid-column: 1 / 3;
  }

}
</style>
