# Блок 8. Основы JavaScript - Циклы (3.2 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Использовать различные типы циклов (for, for...of, for...in, while)
- Понимать разницу между циклами и когда какой использовать
- Применять break и continue для управления циклами
- Работать с вложенными циклами
- Оптимизировать производительность циклов

---

## 📚 Теоретическая часть

### 1. Цикл for

Классический цикл с инициализацией, условием и инкрементом.

```javascript
// Базовый синтаксис: for (инициализация; условие; инкремент)
for (let i = 0; i < 5; i++) {
    console.log(`Итерация ${i}`);
}

// Обход массива
let fruits = ['apple', 'banana', 'orange'];
for (let i = 0; i < fruits.length; i++) {
    console.log(`${i}: ${fruits[i]}`);
}

// Обратный обход
for (let i = fruits.length - 1; i >= 0; i--) {
    console.log(`${i}: ${fruits[i]}`);
}

// Шаг больше 1
for (let i = 0; i < 10; i += 2) {
    console.log(`Четное число: ${i}`);
}

// Множественные переменные
for (let i = 0, j = 10; i < j; i++, j--) {
    console.log(`i: ${i}, j: ${j}`);
}

// Пустые части цикла
let k = 0;
for (; k < 3;) {
    console.log(k);
    k++;
}
```

### 2. Цикл for...of

Современный способ итерации по итерируемым объектам.

```javascript
// Обход массива
let numbers = [1, 2, 3, 4, 5];
for (let number of numbers) {
    console.log(number);
}

// Обход строки
let text = "Hello";
for (let char of text) {
    console.log(char);
}

// Обход с индексом
let colors = ['red', 'green', 'blue'];
for (let [index, color] of colors.entries()) {
    console.log(`${index}: ${color}`);
}

// Обход Set
let uniqueNumbers = new Set([1, 2, 3, 2, 1]);
for (let num of uniqueNumbers) {
    console.log(num); // 1, 2, 3
}

// Обход Map
let userRoles = new Map([
    ['john', 'admin'],
    ['jane', 'user'],
    ['bob', 'moderator']
]);

for (let [username, role] of userRoles) {
    console.log(`${username}: ${role}`);
}

// Обход только ключей или значений Map
for (let username of userRoles.keys()) {
    console.log(`User: ${username}`);
}

for (let role of userRoles.values()) {
    console.log(`Role: ${role}`);
}
```

### 3. Цикл for...in

Итерация по перечисляемым свойствам объекта.

```javascript
// Обход объекта
let person = {
    name: 'John',
    age: 30,
    city: 'Moscow'
};

for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}

// Проверка собственных свойств
let child = Object.create(person);
child.school = 'High School';

for (let key in child) {
    if (child.hasOwnProperty(key)) {
        console.log(`Own property - ${key}: ${child[key]}`);
    } else {
        console.log(`Inherited property - ${key}: ${child[key]}`);
    }
}

// for...in с массивами (не рекомендуется!)
let arr = ['a', 'b', 'c'];
arr.customProperty = 'custom';

for (let index in arr) {
    console.log(`${index}: ${arr[index]}`);
    // Выведет: 0: a, 1: b, 2: c, customProperty: custom
}

// Лучше использовать for...of для массивов
for (let value of arr) {
    console.log(value); // a, b, c (без customProperty)
}
```

### 4. Цикл while

Выполняется пока условие истинно.

```javascript
// Базовый while
let i = 0;
while (i < 5) {
    console.log(`i = ${i}`);
    i++;
}

// Чтение данных до определенного условия
let input = '';
while (input !== 'exit') {
    input = prompt('Введите команду (exit для выхода):') || '';
    console.log(`Вы ввели: ${input}`);
}

// Поиск элемента
let numbers = [1, 3, 5, 7, 9, 2, 4];
let target = 7;
let index = 0;
let found = false;

while (index < numbers.length && !found) {
    if (numbers[index] === target) {
        found = true;
        console.log(`Найден элемент ${target} на позиции ${index}`);
    }
    index++;
}

// Обработка вложенных структур
let data = [
    [1, 2, 3],
    [4, 5],
    [6, 7, 8, 9]
];

let outerIndex = 0;
while (outerIndex < data.length) {
    let innerIndex = 0;
    while (innerIndex < data[outerIndex].length) {
        console.log(data[outerIndex][innerIndex]);
        innerIndex++;
    }
    outerIndex++;
}
```

### 5. Цикл do...while

Выполняется минимум один раз, затем проверяется условие.

```javascript
// Базовый do...while
let count = 0;
do {
    console.log(`Count: ${count}`);
    count++;
} while (count < 3);

// Меню программы
let choice;
do {
    console.log('1. Добавить элемент');
    console.log('2. Удалить элемент');
    console.log('3. Показать список');
    console.log('0. Выход');
    
    choice = parseInt(prompt('Выберите опцию:') || '0');
    
    switch (choice) {
        case 1:
            console.log('Добавление элемента...');
            break;
        case 2:
            console.log('Удаление элемента...');
            break;
        case 3:
            console.log('Показ списка...');
            break;
        case 0:
            console.log('Выход из программы');
            break;
        default:
            console.log('Неверный выбор');
    }
} while (choice !== 0);

// Валидация ввода
let password;
do {
    password = prompt('Введите пароль (минимум 6 символов):') || '';
    if (password.length < 6) {
        console.log('Пароль слишком короткий!');
    }
} while (password.length < 6);
```

### 6. Управление циклами: break и continue

```javascript
// break - выход из цикла
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break; // Выход из цикла при i = 5
    }
    console.log(i); // 0, 1, 2, 3, 4
}

// continue - пропуск итерации
for (let i = 0; i < 10; i++) {
    if (i % 2 === 0) {
        continue; // Пропуск четных чисел
    }
    console.log(i); // 1, 3, 5, 7, 9
}

// Поиск с break
let users = ['john', 'jane', 'bob', 'alice'];
let searchUser = 'bob';
let userFound = false;

for (let user of users) {
    if (user === searchUser) {
        console.log(`Пользователь ${user} найден!`);
        userFound = true;
        break;
    }
}

// Фильтрация с continue
let numbers = [1, -2, 3, -4, 5, -6, 7];
let positiveSum = 0;

for (let num of numbers) {
    if (num < 0) {
        continue; // Пропускаем отрицательные числа
    }
    positiveSum += num;
}
console.log(`Сумма положительных чисел: ${positiveSum}`); // 16

// Метки для вложенных циклов
outer: for (let i = 0; i < 3; i++) {
    inner: for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 1) {
            break outer; // Выход из внешнего цикла
        }
        console.log(`i: ${i}, j: ${j}`);
    }
}
```

### 7. Вложенные циклы

```javascript
// Таблица умножения
for (let i = 1; i <= 10; i++) {
    let row = '';
    for (let j = 1; j <= 10; j++) {
        row += `${i * j}\t`;
    }
    console.log(row);
}

// Обход двумерного массива
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
        console.log(`matrix[${i}][${j}] = ${matrix[i][j]}`);
    }
}

// Поиск в двумерном массиве
let target = 5;
let found = false;

for (let i = 0; i < matrix.length && !found; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
        if (matrix[i][j] === target) {
            console.log(`Найден элемент ${target} в позиции [${i}][${j}]`);
            found = true;
            break;
        }
    }
}

// Генерация комбинаций
let colors = ['red', 'green', 'blue'];
let sizes = ['S', 'M', 'L'];

for (let color of colors) {
    for (let size of sizes) {
        console.log(`${color} ${size}`);
    }
}
```

---

## 💻 Практические упражнения

### Упражнение 1: Основные циклы (45 минут)

```javascript
// 1. Числовые последовательности
function generateSequence(start, end, step = 1) {
    // Сгенерируйте последовательность чисел от start до end с шагом step
    // Используйте цикл for
}

function fibonacci(n) {
    // Сгенерируйте первые n чисел Фибоначчи
    // Используйте цикл while или for
}

function factorial(n) {
    // Вычислите факториал числа n
    // Используйте любой цикл
}

// 2. Работа со строками
function countVowels(str) {
    // Подсчитайте количество гласных в строке
    // Используйте for...of
}

function reverseString(str) {
    // Переверните строку используя цикл
    // Не используйте встроенные методы
}

function isPalindrome(str) {
    // Проверьте, является ли строка палиндромом
    // Используйте цикл for с двумя указателями
}

// 3. Поиск и фильтрация
function findMax(numbers) {
    // Найдите максимальное число в массиве
    // Используйте for...of
}

function findAllIndices(arr, target) {
    // Найдите все индексы элемента target в массиве
    // Используйте цикл for с индексами
}

function filterEven(numbers) {
    // Отфильтруйте четные числа используя цикл
    // Не используйте метод filter
}

// Тестирование
console.log(generateSequence(1, 10, 2)); // [1, 3, 5, 7, 9]
console.log(fibonacci(8)); // [0, 1, 1, 2, 3, 5, 8, 13]
console.log(factorial(5)); // 120

console.log(countVowels("Hello World")); // 3
console.log(reverseString("JavaScript")); // "tpircSavaJ"
console.log(isPalindrome("racecar")); // true

console.log(findMax([3, 7, 2, 9, 1])); // 9
console.log(findAllIndices([1, 2, 3, 2, 4, 2], 2)); // [1, 3, 5]
console.log(filterEven([1, 2, 3, 4, 5, 6])); // [2, 4, 6]
```

### Упражнение 2: Работа с объектами и сложными структурами (50 минут)

```javascript
// 1. Обработка объектов
function getObjectInfo(obj) {
    // Используя for...in, верните информацию об объекте:
    // { keys: [...], values: [...], entries: [...], count: number }
}

function deepClone(obj) {
    // Создайте глубокую копию объекта используя циклы
    // Обработайте вложенные объекты и массивы
}

function mergeObjects(...objects) {
    // Слейте объекты используя for...of и for...in
    // Последние значения должны перезаписывать предыдущие
}

// 2. Работа с массивами объектов
let students = [
    { name: 'John', age: 20, grades: [85, 90, 78] },
    { name: 'Jane', age: 19, grades: [92, 88, 94] },
    { name: 'Bob', age: 21, grades: [76, 82, 80] }
];

function calculateAverages(students) {
    // Вычислите средний балл для каждого студента
    // Используйте вложенные циклы
}

function findTopStudent(students) {
    // Найдите студента с наивысшим средним баллом
    // Используйте циклы для вычисления и сравнения
}

function getGradeDistribution(students) {
    // Подсчитайте распределение оценок по диапазонам:
    // A: 90-100, B: 80-89, C: 70-79, D: 60-69, F: <60
}

// 3. Двумерные массивы
let matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
];

function transposeMatrix(matrix) {
    // Транспонируйте матрицу (поменяйте строки и столбцы местами)
}

function findInMatrix(matrix, target) {
    // Найдите элемент в матрице, верните координаты [row, col]
    // Если не найден, верните null
}

function getMatrixSum(matrix) {
    // Вычислите сумму всех элементов матрицы
}

// Тестирование
let testObj = { a: 1, b: { c: 2, d: [3, 4] }, e: 'test' };
console.log(getObjectInfo(testObj));
console.log(deepClone(testObj));

console.log(calculateAverages(students));
console.log(findTopStudent(students));
console.log(getGradeDistribution(students));

console.log(transposeMatrix(matrix));
console.log(findInMatrix(matrix, 7)); // [1, 2]
console.log(getMatrixSum(matrix)); // 78
```

### Упражнение 3: Алгоритмы и оптимизация (40 минут)

```javascript
// 1. Алгоритмы сортировки
function bubbleSort(arr) {
    // Реализуйте сортировку пузырьком
    // Используйте вложенные циклы
}

function selectionSort(arr) {
    // Реализуйте сортировку выбором
}

function insertionSort(arr) {
    // Реализуйте сортировку вставками
}

// 2. Поиск и анализ
function binarySearch(sortedArr, target) {
    // Реализуйте бинарный поиск
    // Используйте цикл while
}

function findDuplicates(arr) {
    // Найдите все дубликаты в массиве
    // Используйте вложенные циклы или объект для подсчета
}

function longestIncreasingSubsequence(arr) {
    // Найдите длину самой длинной возрастающей подпоследовательности
}

// 3. Генерация и валидация
function generatePrimes(limit) {
    // Сгенерируйте все простые числа до limit (решето Эратосфена)
    // Используйте вложенные циклы
}

function validateSudoku(board) {
    // Проверьте корректность судоку (9x9)
    // board - двумерный массив, 0 означает пустую ячейку
}

function generatePermutations(arr) {
    // Сгенерируйте все перестановки массива
    // Используйте рекурсию и циклы
}

// Тестирование
let unsorted = [64, 34, 25, 12, 22, 11, 90];
console.log(bubbleSort([...unsorted]));
console.log(selectionSort([...unsorted]));
console.log(insertionSort([...unsorted]));

let sorted = [1, 3, 5, 7, 9, 11, 13, 15];
console.log(binarySearch(sorted, 7)); // индекс элемента или -1

console.log(findDuplicates([1, 2, 3, 2, 4, 3, 5])); // [2, 3]
console.log(longestIncreasingSubsequence([10, 9, 2, 5, 3, 7, 101, 18])); // 4

console.log(generatePrimes(30)); // [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]

let sudokuBoard = [
    [5,3,0,0,7,0,0,0,0],
    [6,0,0,1,9,5,0,0,0],
    // ... остальные строки
];
// console.log(validateSudoku(sudokuBoard));

console.log(generatePermutations([1, 2, 3])); // [[1,2,3], [1,3,2], [2,1,3], ...]
```

### Упражнение 4: Практические задачи (37 минут)

```javascript
// 1. Обработка данных
function processLogFile(logEntries) {
    // logEntries - массив строк вида "2023-01-01 10:30:15 ERROR User not found"
    // Обработайте лог и верните статистику:
    // { totalEntries, errorCount, warningCount, infoCount, hourlyStats }
}

function analyzeWebsiteTraffic(visits) {
    // visits - массив объектов { timestamp, page, userId, duration }
    // Проанализируйте трафик и верните:
    // { uniqueUsers, popularPages, averageDuration, peakHours }
}

// 2. Игровая логика
function playNumberGuessing() {
    // Реализуйте игру "Угадай число"
    // Компьютер загадывает число от 1 до 100
    // Пользователь угадывает, получая подсказки "больше/меньше"
    // Используйте do...while для игрового цикла
}

function solveMaze(maze, start, end) {
    // maze - двумерный массив (0 - проход, 1 - стена)
    // start, end - координаты [row, col]
    // Найдите путь от start до end
    // Верните массив координат пути или null
}

// 3. Текстовый анализ
function analyzeText(text) {
    // Проанализируйте текст и верните:
    // { wordCount, charCount, sentenceCount, avgWordsPerSentence, mostFrequentWords }
}

function findAnagrams(words) {
    // Найдите все группы анаграмм в массиве слов
    // Верните массив групп: [['eat', 'tea', 'ate'], ['bat', 'tab']]
}

// 4. Математические задачи
function solveQuadratic(a, b, c) {
    // Решите квадратное уравнение ax² + bx + c = 0
    // Используйте циклы для итеративных методов если нужно
}

function calculatePI(precision) {
    // Вычислите π с заданной точностью используя ряд Лейбница
    // π/4 = 1 - 1/3 + 1/5 - 1/7 + 1/9 - ...
}

function matrixMultiply(a, b) {
    // Умножьте две матрицы
    // Используйте тройной вложенный цикл
}

// Тестовые данные
let logData = [
    "2023-01-01 10:30:15 ERROR User not found",
    "2023-01-01 10:31:20 INFO User logged in",
    "2023-01-01 11:15:30 WARNING Low disk space",
    "2023-01-01 11:20:45 ERROR Database connection failed"
];

let trafficData = [
    { timestamp: '2023-01-01T10:30:00Z', page: '/home', userId: 'user1', duration: 120 },
    { timestamp: '2023-01-01T10:35:00Z', page: '/about', userId: 'user1', duration: 60 },
    { timestamp: '2023-01-01T10:40:00Z', page: '/home', userId: 'user2', duration: 90 }
];

let testMaze = [
    [0, 1, 0, 0, 0],
    [0, 1, 0, 1, 0],
    [0, 0, 0, 1, 0],
    [1, 1, 0, 0, 0],
    [0, 0, 0, 1, 0]
];

// Тестирование
console.log(processLogFile(logData));
console.log(analyzeWebsiteTraffic(trafficData));
console.log(solveMaze(testMaze, [0, 0], [4, 4]));
console.log(analyzeText("Hello world. This is a test. Hello again."));
console.log(findAnagrams(['eat', 'tea', 'tan', 'ate', 'nat', 'bat']));
console.log(calculatePI(1000)); // π с точностью до 1000 итераций
```

---

## 🧪 Проверочные вопросы

1. В чем разница между `for...of` и `for...in`?
2. Когда использовать `while` вместо `for`?
3. В чем разница между `break` и `continue`?
4. Что такое метки в циклах и когда их использовать?
5. Почему не рекомендуется использовать `for...in` для массивов?
6. Как оптимизировать производительность вложенных циклов?
7. В каких случаях `do...while` предпочтительнее `while`?

## 📝 Домашнее задание

Создайте консольную игру "Морской бой":

```javascript
// Игра "Морской бой"
class BattleshipGame {
    constructor(size = 10) {
        this.size = size;
        this.playerBoard = this.createBoard();
        this.computerBoard = this.createBoard();
        this.playerShots = this.createBoard();
        this.computerShots = this.createBoard();
        this.ships = [4, 3, 3, 2, 2, 2, 1, 1, 1, 1]; // размеры кораблей
    }
    
    createBoard() {
        // Создайте двумерный массив размером size x size
        // Используйте вложенные циклы
    }
    
    placeShipsRandomly(board) {
        // Разместите корабли случайным образом
        // Используйте циклы для проверки валидности размещения
    }
    
    displayBoard(board, hideShips = false) {
        // Отобразите доску в консоли
        // Используйте вложенные циклы для вывода
    }
    
    makeShot(board, row, col) {
        // Сделайте выстрел по координатам
        // Верните результат: 'miss', 'hit', 'sunk'
    }
    
    isGameOver(board) {
        // Проверьте, все ли корабли потоплены
        // Используйте вложенные циклы
    }
    
    playGame() {
        // Основной игровой цикл
        // Используйте do...while или while
        // Чередуйте ходы игрока и компьютера
    }
}

// Дополнительные утилиты
const GameUtils = {
    getRandomCoordinate(max) {
        // Генерируйте случайные координаты
    },
    
    isValidPlacement(board, row, col, size, direction) {
        // Проверьте, можно ли разместить корабль
        // Используйте циклы для проверки
    },
    
    getAdjacentCells(row, col, boardSize) {
        // Получите соседние клетки
        // Используйте циклы для обхода
    }
};

// Запуск игры
let game = new BattleshipGame();
game.playGame();
```

---

## 🔗 Полезные ссылки

- [Loops and Iteration - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- [for...of Statement - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [for...in Statement - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
- [while Statement - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)

**Время изучения блока: 3.2 часа** 