<template>
  <div class="max-w-xs mx-auto mt-10 p-4 bg-gray-100 rounded-lg shadow-md">
    <div class="mb-4">
      <input type="text"
             readonly
             class="w-full p-3 text-right text-2xl bg-white rounded-lg shadow-inner text-black"
             v-model="displayValue" />
    </div>
    <div class="grid grid-cols-4 gap-2">
      <button v-for="button in buttons"
              :key="button.label"
              class="p-4 text-xl bg-gray-200 rounded-lg hover:bg-gray-300 text-black"
              :class="button.class"
              @click="() => handleClick(button.label)"
              >
        {{ button.label }}
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const displayValue = ref('0');

const buttons = [
  { label: 'C', class: 'col-span-2 bg-red-500 text-white' },
  { label: 'CE', class: 'bg-yellow-500 text-white' },
  { label: '÷', class: 'bg-blue-500 text-white' },
  { label: '7', class: 'bg-gray-200' },
  { label: '8', class: 'bg-gray-200' },
  { label: '9', class: 'bg-gray-200' },
  { label: '×', class: 'bg-blue-500 text-white' },
  { label: '4', class: 'bg-gray-200' },
  { label: '5', class: 'bg-gray-200' },
  { label: '6', class: 'bg-gray-200' },
  { label: '-', class: 'bg-blue-500 text-white' },
  { label: '1', class: 'bg-gray-200' },
  { label: '2', class: 'bg-gray-200' },
  { label: '3', class: 'bg-gray-200' },
  { label: '+', class: 'bg-blue-500 text-white' },
  { label: '0', class: 'col-span-2 bg-gray-200' },
  { label: '.', class: 'bg-gray-200' },
  { label: '=', class: 'bg-green-500 text-white' },
];

function evalExpression() {
  const mappedStr = displayValue.value
    .replace(/÷/g, '/')
    .replace(/×/g, '*');
    try {
      displayValue.value = eval(mappedStr);
    } catch (error) {
      displayValue.value = 'Error';
    }
}

function clearDisplay() {
  displayValue.value = '0';
}

function clearLastEntry() {
  displayValue.value = displayValue.value?.toString().slice(0, -1);
}

function handleClick(key: string) {
  switch (key) {
    case 'C':
      clearDisplay();
      break;
    case 'CE':
      clearLastEntry();
      break;
    case '=':
      evalExpression();
      break;
    default:
      if (displayValue.value === '0') {
        displayValue.value = key;
      } else {
        displayValue.value += key;
      }
      break;
  }
}
</script>
<style scoped></style>
