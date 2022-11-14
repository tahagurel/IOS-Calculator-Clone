<template>
  <div id="app">
    <div class="wrapper">
    <div class="main">
      <div class="display">
        <div v-if="isResultShown">
          {{result}}
        </div>
        <div v-else>
          <div v-if="isCommandClicked"> {{number2}} </div>
          <div v-else>{{number}}</div>
        </div>
      </div>
      <div class="buttons">
        <div>
          <button @click="allClear" class="grey">AC</button>
          <button @click="plusMinus()" class="grey">⁺∕₋</button>
          <button @click="command('%')" class="grey">%</button>
          <button @click="command('/')" class="orange ">÷</button>
        </div>
        <div>
          <button @click="numberCounter(7)" class="darkGrey">7</button>
          <button @click="numberCounter(8)" class="darkGrey">8</button>
          <button @click="numberCounter(9)" class="darkGrey">9</button>
          <button class="orange " @click="command('x')">x</button>
        </div>
        <div>
          <button @click="numberCounter(4)" class="darkGrey">4</button>
          <button @click="numberCounter(5)" class="darkGrey">5</button>
          <button @click="numberCounter(6)" class="darkGrey">6</button>
          <button @click="command('-')" class="orange ">-</button>
        </div>
        <div>
          <button @click="numberCounter(1)" class="darkGrey">1</button>
          <button @click="numberCounter(2)" class="darkGrey">2</button>
          <button @click="numberCounter(3)" class="darkGrey">3</button>
          <button class="orange " @click="command('+')">+</button>
        </div>
        <div>
          <button @click="numberCounter(0)" class="darkGrey zero">0</button>
          <button @click="numberCounter('.') " :disabled="isDotAdded" class="darkGrey">.</button>
          <button @click="command('=')" :disabled="!number2" class="orange ">=</button>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        number: 0,
        number2: 0,
        result: 0,
        isCommandClicked: false,
        isResultShown: false,
        equals: null,
        isDotAdded: false
      }
    },
    components: {},
    methods: {

      numberCounter(val) {
        if (this.isCommandClicked) {
          if (val == '.') {
            this.isDotAdded = true
          }
          if (!this.number2 && val != '.') {
            this.number2 = (this.number2 + val)
          } else {
            this.number2 = (this.number2 + '' + val)
          }
        } else {
          if (val == '.') {
            this.isDotAdded = true
          }
          if (!this.number && val != '.') {
            this.number = (this.number + val)
          } else {
            this.number = (this.number + '' + val)
          }
        }
      },
      commandEquals() {
        switch (this.equals) {
          case '+':
            this.isCommandClicked = true
            this.result = this.number + this.number2
            break;
          case '-':
            this.isCommandClicked = true
            this.result = this.number - this.number2
            break;
          case '/':
            this.result = this.number / this.number2
            break;
          case '%':
            this.result = (this.number * this.number2) / 100
            break;
          case 'x':
            this.isCommandClicked = true
            this.result = this.number * this.number2
            break;
          default:
            break;
        }
        this.number2 = 0
        this.number = this.result
        this.isResultShown = true
        this.isDotAdded = false
      },
      command(command) {
        this.isCommandClicked = true
        this.number = parseFloat(this.number)
        this.number2 = parseFloat(this.number2)
        this.isResultShown = false
        this.isDotAdded = false
        if (command == '=') {
          this.commandEquals()
        } else {
          this.equals = command
        }
      },
      allClear() {
        this.isCommandClicked = false
        this.number = 0
        this.number2 = 0
        this.result = 0
        this.isResultShown = false
      },
      plusMinus() {
        if (!this.isCommandClicked) {
          this.number = this.number * -1
        } else {
          this.number2 = this.number2 * -1
        }
      },
    }
  }
</script>

<style>
  body {
    background-color: black;
  }

  button {
    font-size: 40px;
    width: 90px;
    height: 90px;
    border-radius: 45px;
    border-color: black;
  }
  .wrapper{
    display: flex;
    justify-content: center;
  }

  .main {
    position: absolute;
    bottom: 20px;
  }

  .display {
    color: #F5F6F6;
    background-color: black;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    font-size: 70px;
    padding-right: 20px;
    font-family: sans-serif;
    font-size: 85px;
  }

  .buttonWrapper {
    display: flex;
    justify-content: space-around;
    text-align: center;
  }

  .buttons {

    text-align: center;
  }

  .orange {
    background-color: #F69906;
    color: #F5F6F6;
  }

  .grey {
    background-color: #9F9F9F;
    color: #020202
  }

  .darkGrey {
    background-color: #313131;
    color: #F8F8F8;
  }

  .zero {
    width: 180px;
    text-align: left;
    padding-left: 35px;
  }
</style>