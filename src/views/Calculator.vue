<template>
  <section>
    <div class="content">
      <div class="calculator">
        <div class="wrapper">
          <div class="result">
            <input class="query" type="text" v-model="query">
            <input class="output" type="text" v-model="result">
          </div>
          <div class="numbers">
            <div class="row 4" @click="test($event)">
              <div class="item">7</div>
              <div class="item">8</div>
              <div class="item">9</div>
              <div class="item action">÷</div>
            </div>
            <div class="row 3" @click="test($event)">
              <div class="item">4</div>
              <div class="item">5</div>
              <div class="item">6</div>
              <div class="item action">x</div>
            </div>
            <div class="row 2" @click="test($event)">
              <div class="item">1</div>
              <div class="item">2</div>
              <div class="item">3</div>
              <div class="item action">-</div>
            </div>
            <div class="row 1" @click="test($event)">
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
      query: ''
    }
  },
  methods: {
    test (event) {
      const functions = {
        '+': (number1, number2) => {
          return number1 + number2
        },
        '-': (number1, number2) => {
          return number1 - number2
        },
        x: (number1, number2) => {
          return number1 * number2
        },
        '÷': (number1, number2) => {
          return number1 / number2
        }
      }

      if (event.toElement.innerText === '=') {
        const length = this.query.length
        let firstNumber = ''
        let operator = ''
        let secondNumber = ''
        for (let i = 0; i < length; i++) {
          if (isNaN(this.query[i])) {
            if (isNaN(this.query[i]) && event.toElement.innerText !== '=') operator = this.query[i]
          }else secondNumber += Number(this.query[i])
          } else firstNumber += Number(this.query[i])
        }
        console.log(operator)
        this.result = functions[operator](firstNumber, secondNumber)
      } else this.query += event.toElement.innerText
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
        border: 1px solid;
        outline: none;
      }
      .output {
        text-align: left;
        border: none;
        outline: none;
        width: 70px;
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
