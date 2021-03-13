<template>
  <section>
    <div class="content">
      <div class="calculator">
        <div class="wrapper">
          <div class="result">
            <input class="query" type="text" v-model="query">
          </div>
          <div class="numbers">
            <div class="row 4" @click="test($event.target.textContent)">
              <div class="item">7</div>
              <div class="item">8</div>
              <div class="item">9</div>
              <div class="item action">÷</div>
            </div>
            <div class="row 3" @click="test($event.target.textContent)">
              <div class="item">4</div>
              <div class="item">5</div>
              <div class="item">6</div>
              <div class="item action" @click="test('*')">x</div>
            </div>
            <div class="row 2" @click="test($event.target.textContent)">
              <div class="item">1</div>
              <div class="item">2</div>
              <div class="item">3</div>
              <div class="item action">-</div>
            </div>
            <div class="row 1" @click="test($event.target.textContent)">
              <div class="item">0</div>
              <div class="item">.</div>
              <div class="item">=</div>
              <div class="item action">+</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// @ is an alias to /src

export default {
  data () {
    return {
      result: 0,
      query: '',
      operator: '',
      firstNumber: null,
      secondNumber: null
    }
  },
  mounted () {
    document.addEventListener('keypress', (event) => this.test(event.key))
  },
  methods: {
    test (event) {
      const functions = {
        '+': (number1, number2) => {
          return Number(number1) + Number(number2)
        },
        '-': (number1, number2) => {
          return Number(number1) - Number(number2)
        },
        '*': (number1, number2) => {
          return Number(number1) * Number(number2)
        },
        '÷': (number1, number2) => {
          return Number(number1) / Number(number2)
        }
      }
      if (isNaN(event) && event !== '.') {
        if (functions[event]) {
          if (!this.firstNumber) {
            this.firstNumber = Number(this.query)
            this.query = ''
            this.operator = event
          } else {
            this.operator = event
            this.secondNumber = Number(this.query)
            const result = functions[this.operator](this.firstNumber, this.secondNumber)
            this.query = result
            this.firstNumber = result
          }
        } else if (event === '=' || event === 'Enter') {
          this.result = functions[this.operator](this.firstNumber, this.query)
          this.query = this.result
          console.log(this.result)
          this.firstNumber = this.result
        }
      } else this.query += event
    }
  }
}
</script>

<style lang="scss" scoped>
  .calculator {
    border: 1px solid darkgray;
    width: 300px;
    height: 300px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    .wrapper {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: center;
    }
    .result {
      display: flex;
      justify-content: center;
      margin-bottom: 10px;
      .query {
        text-align: right;
        border: 1px solid;
        outline: none;
      }
    }
  }
  .numbers {
    display: flex;
    flex-direction: column;
    justify-content: center;
    .row {
      display: flex;
      justify-content: center;
      align-items: flex-end;
      width: auto;
      .item {
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        border: 1px solid red;
        width: 50px;
        height: 50px;
        padding: 5px;
      }
    }
  }
</style>
