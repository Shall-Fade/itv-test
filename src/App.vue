<template>
  <div class="h-screen grid text-[18px]">
    <!-- ПЕРВОЕ ЗАДАНИЕ -->
    <section class="p-[20px] bg-[lightgreen]">
      <h2 class="font-bold text-[42px] mb-[10px]">Первое задание</h2>
      <p><b>Заданный массив:</b> {{ data }}</p>
      <p><b>Результат:</b> {{ resultArr }}</p>
    </section>
    <!-- ВТОРОЕ ЗАДАНИЕ -->
    <section class="p-[20px] bg-[lightblue]">
      <h2 class="font-bold text-[42px] mb-[10px]">Второе задание</h2>
      <form @submit.prevent="convertNumber()" class="flex flex-col">
        <input
          class="outline-none px-[25px] py-[15px] rounded-[10px] mb-[10px]"
          v-model="enteredNumber"
          type="text"
          placeholder="Введите число..."
        />
        <span class="font-bold text-[20px]">Результат: {{ result }}</span>
      </form>
    </section>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Variables
const result = ref();
let resultArr = [];
const enteredNumber = ref();
const alphabet = "abcdefghijklmnopqrstuvwxyz";
let data = [
  {
    id: 0,
    parent_id: null,
  },
  {
    id: 1,
    parent_id: 2,
  },
  {
    id: 2,
    parent_id: 0,
  },
  {
    id: 4,
    parent_id: 1,
  },
  {
    id: 5,
    parent_id: 1,
  },
  {
    id: 6,
    parent_id: null,
  },
  {
    id: 7,
    parent_id: 6,
  },
];

// ПЕРВОЕ ЗАДАНИЕ
// Create a tree from a flat array
function createTree(array, parent_id = null) {
  resultArr = array
    .filter((item) => item.parent_id === parent_id)
    .map((item) => ({ ...item, childs: createTree(array, item.id) }));

  resultArr.map((item) => delete item["parent_id"]);

  return resultArr;
}

console.log("Результат первого задания: ");
console.log(createTree(data));

// ВТОРОЕ ЗАДАНИЕ
// Convert a number to excel column coordinate
function convertNumber() {
  let lettersArray = alphabet.split("");
  let countIndex = Math.floor(enteredNumber.value / 26);
  let letterIndex = enteredNumber.value % 26;

  if (countIndex === 0) {
    result.value = lettersArray[letterIndex - 1].toUpperCase();
  } else if (countIndex === 1 && letterIndex === 0) {
    result.value = lettersArray[25].toUpperCase();
  } else if (countIndex >= 1 && letterIndex === 0) {
    result.value = `${lettersArray[
      countIndex - 1
    ].toUpperCase()}${lettersArray[25].toUpperCase()}`;
  } else {
    result.value = `${lettersArray[countIndex - 1].toUpperCase()}${lettersArray[
      letterIndex - 1
    ].toUpperCase()}`;
  }

  console.log("Результат второго задания: " + result.value);
}
</script>
