<template>
  <div class="calculator App">
    <table cellspacing = "10">

      <tr>
        <td colspan="4">
          <input type="text" disabled v-model="result">
        </td>
      </tr>

      <tr>
        <td class="btn darker" @click="clear">C</td>
        <td class="btn darker" @click="sign">+/-</td>
        <td class="btn darker" @click="percentage">%</td>
        <td class="btn orange" @click="setOperator('/')">/</td>
      </tr>

      <tr>
        <td class="btn grey" @click="addNumber(7)">7</td>
        <td class="btn grey" @click="addNumber(8)">8</td>
        <td class="btn grey" @click="addNumber(9)">9</td>
        <td class="btn orange" @click="setOperator('*')">X</td>
      </tr>

      <tr>
        <td class="btn grey" @click="addNumber(4)">4</td>
        <td class="btn grey" @click="addNumber(5)">5</td>
        <td class="btn grey" @click="addNumber(6)">6</td>
        <td class="btn orange" @click="setOperator('-')">-</td>
      </tr>

      <tr>
        <td class="btn grey" @click="addNumber(1)">1</td>
        <td class="btn grey" @click="addNumber(2)">2</td>
        <td class="btn grey" @click="addNumber(3)">3</td>
        <td class="btn orange" @click="setOperator('+')">+</td>
      </tr>

      <tr>
        <td class="btn-col-2 grey" colspan="2" @click="addNumber(0)">0</td>
        <td class="btn grey" @click="addPoint()">.</td>
        <td class="btn orange" @click="equal()">=</td>
      </tr>

      <tr>
        <td class="btn-col-2 orange" colspan="2"  @click="setOperator('^')">^</td>
        <td class="btn-col-2 orange" colspan="2" @click="setOperator('√')">√</td>
      </tr>

    </table>
  </div>
</template>

<script>
export default {
  data: function() {
    return{
      result: 0,
      tmp_value: 0,
      reset: false,
      operator: undefined

    }
  },
  methods: {
    clear() {
      this.result = 0;
      this.tmp_value = 0;
      this.operator = undefined;
    },

    sign() {
      this.result *= -1;
    },

    percentage() {
      this.result /= 100;
    },

    addNumber(number) {
            if(this.result == 0 || this.reset === true) {
              this.result = '';
              this.reset = false;
            }
            this.result += number.toString();
    },

    addPoint() {
        if(!this.result.includes('.'))
          this.result += '.';
      },

      setOperator(operator) {
        if(this.tmp_value != 0)
          this.calculate();
        this.tmp_value = this.result;
        this.operator = operator;
        this.reset = true;
      },

      equal() {
        this.calculate();
        this.tmp_value = 0;
        this.operator = undefined;
      },

      calculate() {
        let value = 0;
        let a = parseFloat(this.tmp_value);
        let b = parseFloat(this.result);
        let c = parseFloat(2);
        let d = parseFloat(1/2);
        switch(this.operator) {
          case '+':
            value = a + b;
            break;
          case '-':
            value = a - b 
            break;
          case '*':
            value = a * b;
            break;
          case '/':
            value = a / b;
            break;
          case '^':
            value = a ** c;
            break;
          case '√':
            value = a ** d;
        }
        this.result = value.toString();
      }
  }
}
</script>

<style lang="css" scoped>
  .calculator {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-size: 3rem;
  }

  table {
    color: #fff;
    width: 370px;
  }

  input {
    display: block;
    width: calc(100% - 30px);
    height: 75px;
    padding: 5px 20px 0px;
    margin-bottom: 10px;
    border: none;
    background-color: #222;
    color: white;
    font-size: 4rem;
    text-align: right;
  }

  .btn {
    margin: 10px;
    border-radius: 40px;
    width: 80px;
    height: 80px;
    text-align: center;
    font-weight: bold;
    cursor: pointer;
  }

  .btn-col-2 {
    border-radius: 40px;
    width: 160px;
    height: 80px;
    text-align: center;
    font-weight: bold;
    cursor: pointer;
  }

  .grey {
    background-color: #ccc;
    color: #333;
  }

  .grey:hover {
    background-color: #333;
    color: #ccc;
  }

  .darker {
    background-color: #444;
    color: white;
  }

  .darker:hover {
    background-color: #555;
  }

  .orange {
    background-color: #e08d1f;
    color: #fff;
  }

  .orange:hover {
    background-color: #fda22f;
  }


</style>