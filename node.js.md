Памятка по синтаксису `JavaScript` для [node.js](https://github.com/nodejs/node) в примерах.

- [Переменные](#переменные)
- [Типы данных](#типы-данных)
- [Функции](#функции)
- [Условия](#условия)
- [Обработка ошибок](#обработка-ошибок)
- [Массивы](#массивы)
- [Объекты](#объекты)
- [Циклы](#циклы)
- [Регулярные выражения](#регулярные-выражения)
- [Math](#math)
- [Асинхронные операции](#асинхронные-операции)

### Переменные

Переменная `var` поддерживает любую область видимости и ее возможно объявить повторно (считается устаревшим методом и рекомендуется не использовать).

```js
console.log(varVariable) // Uncaught ReferenceError: varVariable is not defined (не определена)
if (true) {
    var varVariable = true
}
console.log(varVariable) // true
var varVariable = 123
console.log(varVariable) // 123
```

Переменная `let` позволяет изменять содержимое с другим типом данных (в отличии от `const`), но ограничина областью видимости (в отличии от `var`).

```js
console.log(letVariable) // Uncaught ReferenceError: letVariable is not defined
if (true) {
    let letVariable = 'letVariable is defined'
}
console.log(letVariable) // Uncaught ReferenceError: letVariable is not defined
let letVariable = 'string'
console.log(letVariable)
let letVariable = 'string' // Uncaught SyntaxError: Identifier 'letVariable' has already been declared (идентификатор уже объявлен)
letVariable = 123
console.log(letVariable)
```

Переменная `const` требует обязательной инициализации, и не позволяет изменять значение переменной после ее объявления.

```js
const constVariable = 'string'
constVariable = '123' // Uncaught TypeError: Assignment to constant variable (ошибка присвоения значения к постоянной переменной)
```

### Типы данных

```js
typeof 32 // number
typeof 3.2 // number
typeof 123n // bigint
typeof 'text' // string
typeof true // boolean
typeof false // boolean
typeof null // object
typeof { key: 'value' } // object
typeof [1, 2, 3] // object
typeof function() {} // function
typeof Symbol('id') // symbol
```

Преобразовать аргумент в число. Возвращает `NaN`, если преобразование невозможно.

```js
Number("123")      // 123
Number("123.45")   // 123.45
Number("abc")      // NaN
Number(undefined)  // NaN
Number(true)       // 1
Number(false)      // 0
Number(null)       // 0
```

Преобразовать строку в целое число. Прекращает чтение, как только встречает нецифровой символ.

```js
parseInt("123abc")  // 123
parseInt("12.34")   // 12
parseInt("abc123")  // NaN
```

Преобразовать строку в число с плавающей точкой.

```js
parseFloat("123.45abc")  // 123.45
parseFloat("abc123.45")  // NaN
```

Преобразовать значение в строку.

```js
(123).toString()   // "123"
(true).toString()  // "true"
String(123)        // "123"
String(true)       // "true"
String(false)      // "false"
String(null)       // "null"
String(undefined)  // "undefined"
```

Преобразовать значение в булевое (логическое) значение. Все значения, кроме `0`, `null`, `NaN`, `undefined` и пустой строки, преобразуются в `true`.

```js
Boolean(123)        // true
Boolean("Hello")    // true
Boolean(0)          // false
!0                  // true
!!0                 // false
Boolean(null)       // false
Boolean(NaN)        // false
Boolean(undefined)  // false
Boolean("")         // false
```

### Функции

```js
function sum (param1, param2) {
    console.log(param1*param2)
}

sum(2,2) // 4

function getRandomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min
}

getRandomInt(1,100) // Например, 44
```

### Условия

```js
function functionName (paramName) {
    if (paramName < 10) {
        console.log(`${paramName} меньше 10`)
    }
    else if (paramName >= 10) {
        console.log(`${paramName} больше или равно 10`)
    }
    else {
        console.log(`Переданное значение - ${paramName} - не подходит под заданные условия`)
    }
}

functionName(5)       // 5 меньше 10
functionName(15)      // 15 больше или равно 10
functionName('test')  // Переданное значение - test - не подходит под заданные условия
```

### Обработка ошибок

```js
function errorTest(a, b) {
    // Блок кода, который будет выполняется до тех пор, пока не возникнет ошибка
    try {
        if (b === 0) {
            throw new Error("на ноль делить нельзя")
        }
        console.log(a / b) // выполняется, если ошибок нет
    }
    // Блок кода, который будет выполнен, если в блоке try возникнет ошибка
    catch (error) {
        console.log(`Ошибка: ${error.message}`) // Обработка ошибки
    }
    // Блок кода, который выполняется в любом случае
    finally {
        console.log("Блок finally выполняется всегда") // Всегда выполняется
    }
}

errorTest(10, 2) 
// 5
// Блок finally выполняется всегда

errorTest(10, 0)
// Ошибка: на ноль делить нельзя
// Блок finally выполняется всегда
```

### Массивы

Классический массив и его методы.

```js
const array = [3, 2, 'string']
Array.isArray(array) // Проверка, является ли переменная массивом (true)
array[2] = 1 // Изменить содержимое элемента в массиве по индексу
array.sort() // сортировка по умолчанию: [ 1, 2, 3 ]
array[0] + array[1] + array[2] // 6
array[3] // undefined (не определено)
array[3] = 4 // Добавить новый элемент в массив по индексу
array.push(5) // Добавить новый элемент с конца
array[4] // 5
array.unshift(0) // Добавить элемент в начало массива
array.shift() // Удалить первый элемент из массива
array.pop() // Удалить последний элемент из массива
array[array.length-1] // Вывести содержимое последнего элемента в массиве
array.indexOf(1) // Выводит индекс первого вхождения элемента в массив, или -1, если элемент не найден
```

Вложенный массив, а также методы фильтрации и объединения:

```js
const data = [
    { id: 1, name: 'red' },
    { id: 2, name: 'blue' },
]

data.push({id: 3, name: 'green'}) // Добавить новый элемент в массив

const nameArray = data.map(item => item.name) // Пересобрать новый массив

const filterArray = nameArray.filter(item => item.length >= 4) // отфильтровать содержимое массива по длинне содержимого
// [ 'blue', 'green' ]

[...nameArray, ...filterArray] // объеденить два массива
// [ 'red', 'blue', 'green', 'blue', 'green' ]
```

### Объекты

Преобразовать объект в массив и наоборот:

```js
const obj = { a: 1, b: 2, c: 3 }
obj.b // 2
let keys = Object.keys(obj)      // [ 'a', 'b', 'c' ]
let values = Object.values(obj)  // [ 1, 2, 3 ]
const arr = Object.entries(obj)  // [["a", 1], ["b", 2], ["c", 3]]
arr[1][1] // 2
Object.fromEntries(arr)          // { a: 1, b: 2, c: 3 }
```

Используя переменную `const` при объявлении объектов, возможно изменять содержимое дочерних элементов.

```js
const box = {
    height: 8,
    width: 40,
    scrollable: true,
    style: {
        fg: 'white',
        bg: 'black'
    }
}

box.height // 8
box.style // { fg: 'white', bg: 'black' }
box.style.fg // white

box.style.fg = 'blue'
box.style.fg // blue
```

Объекты и вложенные массивы `JavaScript` могут содержать дочерние массивы внутри `[]` и вложенные объекты внутри `{}`.

```js
const obj = [
    'JavaScript',
    2024,
    [
        'Express',
        'Axios',
    ],
    {
        name: 'Alex',
        age: 29,
        num: [1, 'string', {}],
        test: {}
    }
]
```

Конвертация в `JSON`:

```js
const jsonString = JSON.stringify(obj)  // Конвертация из объекта JavaScript в JSON
const obj = JSON.parse(jsonString)      // Конвертация из JSON в JavaScript
```

### Циклы

Примеры циклов взяты из проекта [multranslate](https://github.com/Lifailon/multranslate), для проверки всех строк в массиве и увеличения количества видимых строк с учетом `autowrap`. Имеется две реальных строки, необходимо узнать количество виртуальных строк с учетом длинны символов в строке. Например, если максимальная длинна одной строки составляет, `36`, то на одну реальную строку в `92` символа приходится дополнительно еще `2` виртуальных. Количество найденных виртуальных строк прибавляется к изначально зафиксированному значению количества всех реальных строк.

```js
// На входе 2 строки, разделенные символом \r
const text = "Первая строка\rВторая очень длинная строка, которое будет превышать максимальное значение символов в строке"

// Фиксируем текущее максимальное количество строк и длинну символов в строке с учетом размеров окна
const maxLines = box.height - 2 // 6
const maxChars = box.width - 4  // 36

// Разбиваем текст на массив из строк
const bufferLine = text.split('\r')
// Забираем реальное количество строк (2)
let viewLines = bufferLine.length

// Вывести количество строк в каждой строке массива
bufferLine.map(item => item.length) // [ 13, 92 ]
```

Классический цикл `for` итерирует числами с типом данных `number` (`int` / `integer`). С каждой интерацией объявленное значение (`let i = 0`) увеличивается на заданное количество (`i++` - на единицу), цикл завершается в случае успешного соблюдения условия (`i < bufferLine.length`).

```js
for (let i = 0; i < bufferLine.length; i++) {
    if (bufferLine[i].length > maxChars) {
        // Добавляем одну виртуальную строку без учета остатка символов
        viewLines++
    }
}
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 3
// Уменьшаем значение на 1, для проверки в других циклах
viewLines--

for (let i = 0; i < bufferLine.length; i++) {
    if (bufferLine[i].length > maxChars) {
        // Добавляем все виртуальные строки, с округлением в меньшую сторону
        viewLines += Math.floor(bufferLine[1].length / maxChars)
    }
}
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 4
viewLines -= 2
```

Цикл `for..in` итерирует по индексам массива, с типом данных `string`. Сколько элементов в массиве (`bufferLine.length`), столько и будет индексов (отсчет начинается с нуля).

```js
for (let index in bufferLine) {
    if (bufferLine[Number(index)].length > maxChars) {
        viewLines += Math.floor(bufferLine[1].length / maxChars)
    }
}
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 4
viewLines -= 2
```

Цикл `for..of` итерирует по элементам массива, с уникальным типом данных каждого элемента в массиве.

```js
const array = [1, 'string', {}]
for (let arr of array) {
    console.log(typeof arr)
}
// number
// string
// object

for (let line of bufferLine) {
    console.log(typeof line)
    if (line.length > maxChars) {
        viewLines += Math.floor(bufferLine[1].length / maxChars)
    }
}
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 4
viewLines -= 2
```

Метод массива `forEach` выполняет указанную функцию для каждого элемента в массиве.

```js
bufferLine.forEach(line => {
    if (line.length > maxChars) {
        viewLines += Math.floor(bufferLine[1].length / maxChars)
    }
})
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 4
viewLines -= 2
```

Цикл `while` Выполняет тело цикла `{}` до тех пор, пока условие истинно

```js
let i = 0
while (i < bufferLine.length) {
    if (bufferLine[i].length > maxChars) {
        viewLines += Math.floor(bufferLine[1].length / maxChars)
    }
    i++
}
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 4
viewLines -= 2
```

Цикл `do..while` сначала выполняет тело цикла, а затем проверяет условие, это гарантирует, что интерация будет выполнена как минимум один раз.

```js
i = 0
do {
    if (bufferLine[i].length > maxChars) {
        viewLines += Math.floor(bufferLine[1].length / maxChars)
    }
    i++
} while (i < bufferLine.length)
console.log(`${maxLines} ${maxChars} ${viewLines}`) // 6 36 4
```

### Регулярные выражения

Преобразовать строку в массив из букв (`char`).

```js
let line = "javascript"
let arr = Array.from(str) // ['j', 'a', 'v', 'a',  's', 'c', 'r', 'i', 'p', 't']
```

Метод `split()` используется для преобразования строки в массив.

```js
line = "1,2,3,4,5"              // '1,2,3,4,5'
arr = line.split(",")           // [ '1', '2', '3', '4', '5' ]
```

Метод `join()` используется для объединение массива в строку.

```js
let arrSlice = arr.slice(1, 3)  // Срез, выводит содержимое массива с 1 по 3 индекс (два элемента)
arrSlice.join()                 // Собирает массив в строку: '2,3'
arrSlice.join(" - ")            // '2 - 3'
```

Метод `match()` используется для поиска совпадений с регулярным выражением в строке. Он возвращает массив с найденными совпадениями или `null`, если совпадений не найдено.

```js
let stringForRegex = "Текст для проверки текста"
stringForRegex.match(/текст/)[0]     // Получить содержимое первого совпадения
stringForRegex.match(/текст/).index  // Возвращает порядковый индекс первого совпадения в тексте (19)
stringForRegex.match(/текст/i)[0]    // Возвращает только первое совпадение без учета регистра
stringForRegex.match(/текст/gi)      // Получить массив всех совпадений: [ 'Текст', 'текст' ]

stringForRegex = "2024-10-25"
stringForRegex.match(/(\d{4})-(\d{2})-(\d{2})/) // Группа захвата, которая возвращает полное совпадение, а также значения отдельных групп
// [ '2024-10-25', '2024', '10', '25', index: 0, input: '25-10-2024', groups: undefined ]
```

Метод `search()` возвращает только индекс первого совпадения.

```js
"Текст для проверки текста".search('про') // 10
```

Метод `replace()` заменяет найденные совпадения в строке на другие значения.

```js
stringForRegex = "Текст для замены"
stringForRegex.replace(/для/, "после")              // 'Текст после замены'
stringForRegex.replace(/^т/i, "Этот т")             // 'Этот текст для замены'
stringForRegex.replace(/$/, "!")                    // 'Текст для замены!'
stringForRegex.replace(/(Текст)/, "$1 только")      // 'Текст только для замены'
stringForRegex.replace(/\s[а-яА-Я]{3}/, "")         // 'Текст замены'
stringForRegex.replace(/\s\p{L}+$/u, " кириллицы")  // 'Текст для кириллицы'

stringForRegex = "Text for regex"
stringForRegex.replace(/\s\w{3}/, "")         // Используется для замены любых латинских букв: 'Text regex'
stringForRegex.replace(/\s[a-zA-Z_]{3}/, "")  // эквивалент \w

stringForRegex = "2024-10-25"
stringForRegex = stringForRegex.replace(/(\d{4})-(\d{2})-(\d{2})/,"$3.$2.$1") // Поменять порядок через группы захвата: '25.10.2024'
stringForRegex.replace(/\d{2}\./g, "11.")   // Заменяет найденные две идущие цифры подряд: '11.11.2024'
stringForRegex.replace(/\d{4}/, "2025")     // Заменяет четыре идущие цифры подряд: '25.10.2025'
stringForRegex.replace(/20\d+/, "2025")     // Заменяет 20 и любые идущие за ним цифры: '25.10.2025'
stringForRegex.replace(/10.+/g, "11.2025")  // Заменяет 10 и любое количетво символов идущее за ним: '25.11.2025'
stringForRegex.replace(/\d{2,4}/g, "11")    // Заменяет найденные цифры следующие в порядке от 2 до 4: ('11.11.11')
stringForRegex.replace(/[45]/g, "1")        // Заменить 4 или 5 на 1: '21.10.2021'
```

### Math

```js
Math.min(9, 10)        // Получить наименьшее значение двух чисел: 9
Math.max(9, 10)        // Получить максимальное значение двух чисел: 10
Math.floor(10 / 3)     // Округлить в меньшую сторону: 3
Math.ceil(10/3)        // Откруглить в большую сторону: 4
Math.trunc(4.9)        // Отбрасывание дробной части: 4
Math.round(4.5)        // Округление до ближайшего целого: 5
Math.round(4.45)       // Округление до ближайшего целого: 4
Math.fround(5.05)      // Ближайшее число с плавающей точкой одинарной точности: 5.050000190734863
Math.random()          // Псевдослучайное число между 0 и 1, например, 0.2309471255442206
Math.abs(-7)           // Получить абсолютное значение: 7
Math.sign(-3)          // Определение знака числа (-1, 0, 1): -1
Math.pow(2, 3)         // Возведение в степень: 8
Math.sqrt(16)          // Квадратный корень: 4
Math.cbrt(27)          // Кубический корень: 3
Math.imul(2, 4)        // Целочисленное 32-битное умножение: 8
Math.clz32(1)          // Количество ведущих нулей в 32-битном представлении: 31
```

### Асинхронные операции

`Promise` (промис) — это объект, который используется для обработки асинхронных операций, позволяя работать с результатами, когда они станут доступны, не блокируя основной поток выполнения. Он может находиться в одном из трех состояний:

- `Pending` (Ожидание): Операция только отправлена на выполнение или еще выполняется.
- `Fulfilled` (Выполнен): Операция завершилась успешно.
- `Rejected` (Отклонен): Операция завершилась с ошибкой.

С помощью ключевых слов `resolve` (разрешить/успех) и `reject` (отклонить/ошибка) производится управление возвращаемым результатом выполнения.

```js
let testPromise = new Promise((resolve, reject) => {
    if (true) {
        resolve("Операция выполнена успешно")
    } else {
        reject("Ошибка выполнения операции")
    }
})

testPromise.then(result => console.log(result)).catch(error => console.error(error))
```

Метод `then` используется для обработки успешного выполнения промиса (в состоянии `fulfilled`).

Метод `catch` используется для обработки ошибок или отказов промиса (в состоянии `rejected`).

`async` — это ключевое слово, которое делает функцию асинхронной и позволяет использовать `await`, чтобы приостановить выполнение до тех пор, пока все промисы не будут выполнены.

`await` — это ключевое слово, которое используется внутри асинхронной функции (async). Оно заставляет ждать выполнения промиса и возвращает его результат.

```js
// Импортируем функцию exec из модуля child_process, которая позволяет запускать команды операционной системы
const { exec } = require('child_process')

// Основная функция выполнения команды ping в промис
function pingHost(host) {
    return new Promise((resolve) => {
        // Выполняем команду ping для указанного хоста с timeout 50 мс
        exec(`ping -n 1 -w 50 ${host}`, (error) => {
            // Если нет ошибки, значит хост отвечает (alive: true)
            if (!error) {
                resolve({ host, alive: true })
            }
            // Если есть ошибка, хост не отвечает (alive: false)
            else {
                resolve({ host, alive: false })
            }
        })
    })
}

// Асинхронная функция создания промисов и получения результатов
async function pingSubnet(subnet) {
    // Массив для хранения промисов
    const promises = []
    // Генерация и пинг каждого IP-адреса в диапазоне от 1 до 254
    for (let i = 1; i <= 254; i++) {
        // Формируем IP-адрес, заменяя последний октет подсети
        const host = `${subnet.split('.').slice(0,3).join('.')}.${i}`
        // Добавляем промис в массив для выполнения пинга в фоне и продолжения интерации
        promises.push(pingHost(host)) // Promise { <pending> }
    }
    // Ждем завершения выполнения всех промисов
    const results = await Promise.all(promises)
    results.forEach(result => {
        if (result.alive) {
            console.log(`+++ ${result.host}`)
        } else {
            console.log(`- ${result.host}`)
        }
    })
}

pingSubnet('192.168.3.0')
```

Использовать внешнюю библиотеку [ping](https://www.npmjs.com/package/ping): `npm install ping`

```js
const ping = require('ping')

// Асинхронная функция отправки команды ping через библиотеку
async function pingHost(host) {
    try {
        const res = await ping.promise.probe(host, { timeout: 1 })
        return { host, alive: res.alive }
    } catch (error) {
        return { host, alive: false }
    }
}

// Функция возврата промисов вручную без async
function pingHost(host) {
    return ping.promise.probe(host, { timeout: 1 })
        .then(res => {
            return { host, alive: res.alive }
        })
        .catch(error => {
            return { host, alive: false }
        })
}

async function pingSubnet(subnet) {
    const promises = []
    for (let i = 1; i <= 254; i++) {
        const host = `${subnet.split('.').slice(0,3).join('.')}.${i}`
        promises.push(pingHost(host))
    }
    const results = await Promise.all(promises)
    results.forEach(result => {
        if (result.alive) {
            console.log(`+++ ${result.host}`)
        } else {
            console.log(`- ${result.host}`)
        }
    })
}

pingSubnet('192.168.3.0')
```

`await Promise.all()` - дожидается успешного выполнения всех запросов.
`await Promise.allSettled()` - дожидается выполнения всех запросов не зависимо от успеха (возвращает статус и результат).
`await Promise.race()` - дожидается первого успешного выполнения, что бы получить результат от него не зависимо от его успеха.
