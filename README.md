### Решение находится в файле App.vue
# Первое задание
## Описание
Есть плоский массив с элементами, содержащими уникальный идентификатор и идентификатор родительского элемента, необходимо построить "деревовидную" структуру. Пример:
```
[
    [
        id: [0-9],
        parent_id: [0-9]
    ],
    ...
]
```
Необходимо построить массив вида:
```
[
    [
        id: [0-9],
        childs: [
            [
                id: [0-9],
                childs: [...]
            ],
            ...
        ]
    ],
    ...
];
```

## Результат
### Небольшое пояснение:
Поскольку было невозможно определить родителя в массиве, пришлось создать ключ parent_id со значением null
```
// Variables
let resultArr = [];
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
```

# Второе задание
## Описание
Необходимо конвертировать чиcло в excel координату колонки. Пример:
```
    1 => A
    2 => B
    27 => AA
    28 => AB
    ...
```

## Результат
```
// Variables
const result = ref();
const enteredNumber = ref();
const alphabet = "abcdefghijklmnopqrstuvwxyz";

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
```

# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Vue - Official](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (previously Volar) and disable Vetur
