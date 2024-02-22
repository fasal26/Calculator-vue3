<template>
    <div class="calculator">
      <div class="output">{{ display }}</div>
      <div class="buttons">
        <button v-for="button in buttons" :key="button.text" @click="handleButtonClick(button)">
          {{ button.text }}
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const display = ref('0');
  
  const buttons = [
    { text: '7' }, { text: '8' }, { text: '9' }, { text: '/' },
    { text: '4' }, { text: '5' }, { text: '6' }, { text: '*' },
    { text: '1' }, { text: '2' }, { text: '3' }, { text: '-' },
    { text: '0' }, { text: 'C' }, { text: '=' }, { text: '+' },
  ];
  
  function handleButtonClick(button) {
    const buttonText = button.text;
    if (buttonText === 'C') {
      clearDisplay();
    } else if (buttonText === '=') {
      calculate();
    } else {
      updateDisplay(buttonText);
    }
  }
  
  function updateDisplay(value) {
    if (display.value === '0') {
      display.value = value;
    } else {
      display.value += value;
    }
  }
  
  function clearDisplay() {
    display.value = '0';
  }
  
  function calculate() {
    try {
      const result = eval(display.value);
      display.value = result.toString();
    } catch (error) {
      console.error('Error evaluating expression:', error);
      display.value = 'Error';
    }
  }
  </script>
  
  <style scoped>
  .calculator {
    max-width: 300px;
    margin: 50px auto;
    border: 1px solid #ccc7c7;
    border-radius: 5px;
    padding: 20px;
  }
  
  .output {
    font-size: 2rem;
    margin-bottom: 10px;
    padding: 10px;
    border-radius: 5px;
    text-align: right;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  button {
    padding: 15px;
    font-size: 18px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background-color: #f1de55;
    transition: background-color 0.3s;
  }
  
  button:hover {
    background-color: #d5b841;
  }
  </style>
  