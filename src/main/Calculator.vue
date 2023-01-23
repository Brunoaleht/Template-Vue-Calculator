<template>
  <div class="calculator">
    <DisplayCalc :value="displayValue" />
    <ButtonCalc label="AC" :triple="true" @onCalcClick="clearMemore" />
    <ButtonCalc label="/" :operation="true" @onCalcClick="setOperation" />
    <ButtonCalc label="7" @onCalcClick="addDigit" />
    <ButtonCalc label="8" @onCalcClick="addDigit" />
    <ButtonCalc label="9" @onCalcClick="addDigit" />
    <ButtonCalc label="*" :operation="true" @onCalcClick="setOperation" />
    <ButtonCalc label="4" @onCalcClick="addDigit" />
    <ButtonCalc label="5" @onCalcClick="addDigit" />
    <ButtonCalc label="6" @onCalcClick="addDigit" />
    <ButtonCalc label="-" :operation="true" @onCalcClick="setOperation" />
    <ButtonCalc label="1" @onCalcClick="addDigit" />
    <ButtonCalc label="2" @onCalcClick="addDigit" />
    <ButtonCalc label="3" @onCalcClick="addDigit" />
    <ButtonCalc label="+" :operation="true" @onCalcClick="setOperation" />
    <ButtonCalc label="0" @onCalcClick="addDigit" :double="true" />
    <ButtonCalc label="." @onCalcClick="addDigit" />
    <ButtonCalc label="=" :operation="true" @onCalcClick="setOperation" />
  </div>
</template>

<script>
import ButtonCalc from "../components/Button.vue";
import DisplayCalc from "../components/Display.vue";
export default {
  name: "CalculatorCalc",
  data: function () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0,
    };
  },
  components: {
    ButtonCalc,
    DisplayCalc,
  },
  methods: {
    clearMemore() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;

        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
          if (isNaN(this.values[0]) || !isFinite(this.values[0])) {
            this.clearMemory();
            return;
          }
        } catch (e) {
          this.$emit("onError", e);
        }

        this.values[1] = 0;
        this.displayValue = this.values[0];
        this.operation = equals ? null : operation;
        this.current = equals ? 0 : 1;
        this.clearDisplay = !equals;
      }
    },
    addDigit(n) {
      if (n === "." && this.displayValue.includes(".")) {
        return;
      }
      const clearDisplay =
        this.displayValue === "0" || this.clearDisplay === true;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + n;

      this.displayValue = displayValue;
      this.clearDisplay = false;
      this.values[this.current] = displayValue;

      //if (n !== ".") {
      //const i = this.current;
      //const newValue = parseFloat(displayValue);
      //this.values[i] = newValue;
      //}
    },
  },
};
</script>

<style>
.calculator {
  height: 320px;
  width: 320px;
  border-radius: 5px;
  overflow: hidden;
  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>
