<script setup>
import { ref } from 'vue';

const formula = ref('');
const inputBox = ref('');

// evaluate input formula
function evaluate() {
  try {
    const result = eval(formula.value);
    inputBox.value = result;
    formula.value = result.toString();
  } catch (exception) {
    console.log("Invalid formula", exception);
    inputBox.value = 'ERR';
  }
}

// add number to formula
function add(value) {
  formula.value = formula.value + value;

  const last = formula.value.match(/(\d+(\.\d+)?)(?!.*\d)/)[0];
  inputBox.value = last;

  console.log(formula);
}

// backspace
function backspace() {
  if (inputBox.value === 'ERR') {
    inputBox.value = '';
  } else {
    let str = inputBox.value.toString();
    inputBox.value = str.slice(0, -1);
  }
  let str2 = formula.value.toString();
  formula.value = str2.slice(0, -1);
}

// clear all numbers
function clear() {
  inputBox.value = '';
  formula.value = '';
}
</script>

<template>
  <b-container style="background-color: #FFFFFF; overflow: hidden">
    <b-row style="height: 8rem;"></b-row>
    <b-row class="mb-1">
      <b-col cols="12">
      <b-form-input type="text" v-model="formula" class="s-text"
      style="border: none; text-align: end; background-color: #FFFFFF;" readonly>
      {{ formula }}</b-form-input>
    </b-col>
    </b-row>

    <b-row class="mt-1 mb-3 mx-0">
      <b-col cols="12">
      <b-form-input type="text" v-model="inputBox"
      style="border: none; text-align: end; font-size: 5em; background-color: #FFFFFF;" readonly>
      {{ inputBox }}</b-form-input>
    </b-col>
    </b-row>

    <b-row class="m-2" style="padding: 0 0.5px">
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-clear" @click="clear">AC</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-clear" @click="backspace">
        C</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-per" @click="add('*0.01')">%</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-oper" @click="add('/')">÷</b-button>
      </b-col>
    </b-row>

    <b-row class="m-2" style="padding: 0 0.5px;">
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(7)">7</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(8)">8</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(9)">9</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-oper" @click="add('*')">×</b-button>
      </b-col>
    </b-row>

    <b-row class="m-2" style="padding: 0 0.5px;">
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(4)">4</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(5)">5</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(6)">6</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-oper" @click="add('-')">-</b-button>
      </b-col>
    </b-row>

    <b-row class="m-2" style="padding: 0 0.5px;">
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(1)">1</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(2)">2</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(3)">3</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-oper" @click="add('+')">+</b-button>
      </b-col>
    </b-row>

    <b-row class="m-2" style="padding: 0 0.5px;">
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add(0)">0</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add('00')">00</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button" @click="add('.')">.</b-button>
      </b-col>
      <b-col cols="3" style="padding: 0 2px">
        <b-button class="w-100 button-oper" @click="evaluate">=</b-button>
      </b-col>
    </b-row>
    <b-row style="height: 1rem;"></b-row>
  </b-container>
</template>

<style scoped>
.s-text {
  font-size: 1.5em;
  color: #808080;
}

.button {
  background-color: #FFFFFF;
  color: black;
  border: none;
  border-radius: 15%;
  width: 40vw;
  aspect-ratio: 1;
  font-weight: bold;
  font-size: 2rem;
}

.button:hover {
  background-color: #CCCCCC;
}

.button-oper {
  background-color: #3333FF;
  color: white;
  border: none;
  border-radius: 15%;
  width: 40vw;
  aspect-ratio: 1;
  font-weight: bold;
  font-size: 2rem;
}

.button-oper:hover {
  background-color: #99CCFF;
}

.button-clear {
  background-color: #999999;
  color: white;
  border: none;
  border-radius: 15%;
  width: 40vw;
  aspect-ratio: 1;
  font-weight: bold;
  font-size: 2rem;
}

.button-clear:hover {
  background-color: #CCCCCC;
}

.button-per {
  background-color: #CCCCCC;
  color: white;
  border: none;
  border-radius: 15%;
  width: 40vw;
  aspect-ratio: 1;
  font-weight: bold;
  font-size: 2rem;
}

.button-per:hover {
  background-color: #999999;
}
</style>
