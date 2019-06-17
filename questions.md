# List of (Advanced) JavaScript Questions

I will post here all the questions and tasks which I have found or heard. For each task, I add the following tags:
- _#JS_ (basic JS knowledge)
- _#DJS_ (deep JS knowledge)
- _#AL_ (algorithmic knowledge)
- _#LA_ (layout, HTML, CSS)
- difficult
  - _#NOOB_ (:v:)
  - _MID_ (:muscle:)
  - _#HARD_ (:metal:)
  
---

https://github.com/lydiahallie/javascript-questions/blob/master/README.md

---

Tags: _#AL_ _#MID_

```javascript
/**
 * Дана строка, состоящая из букв A-Z:
 * "AAAABBBCCXYZDDDDEEEFFFAAAAAABBBBBBBBBBBBBBBBBBBBBBBBBBBB"
 * Нужно написать функцию RLE, которая на выходе даст строку вида:
 * "A4B3C2XYZD4E3F3A6B28"
 * И сгенерирует любую ошибку, если на вход пришла невалидная строка.
 *
 * Пояснения:
 * 1. Если символ встречается 1 раз, он остается без изменений
 * 2. Если символ повторяется более 1 раза, к нему добавляется количество повторений
 */

function rle(str) {
    // your code
}
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
function rle(str) {
    if (str.search(/[^A-Z]/) > -1) {
        throw new Error('');
    }

    if (str.length <= 1) {
        return str;
    }
    
    let obj = {};
    let order = 0;
    for (let i = 0, len = str.length; i < len; ++i) {
        const ch = str[i];
        if (obj[ch] === undefined) {
            obj[ch] = {count: 0, ch: ch, order: ++order}
        }
        obj[ch].count += 1;
    }

    let arr = [];
    Object.values(obj).forEach((item) => {
        arr[item.order] = '' + item.ch + (item.count === 1 ? '' : item.count); 
    });
    return arr.join('');
}
```

</p>
</details>

---

Tags: _#DJS_ _#MID_

```javascript
var nums = [ 1, 2, 3, 4, 5 ];
var accumulator = Promise.resolve();

for (var i = 0; i < nums.length; ++i) {
    accumulator = accumulator.then(function(i, result) {
        result = result || 0;
        return result + nums[i];
    });
}

accumulator.then(function(result) {
    console.log(result); // What will be in the console after the execution of this line?
});
```

<details><summary><b>Answer</b></summary>
<p>

- You should pay attention on var in cycle (you should use let)
- You should pay attention on i after all iterations (i == 5)
- You should know what will be after undefined + number in line 6 (NaN)

</p>
</details>

---

Tags: _#DJS_ _#HARD_

```javascript
sum(1);       // => 1
sum(1)(2);    // => 3
sum(1)(2)(3); // => 6


function sum(n) {
    // your code
}
```

<details><summary><b>Answer</b></summary>
<p>

- You should override two methods: valueOf and toString
- You should return function
- You shouldn't use bind

```javascript
function sum(n) {
    let value = n;
    function B(k) {
        value = value + k;
        return B;
    }
    B.valueOf = function() {
        return value;
    };
    B.toString = function() {
        return '' + value;
    };
    return B
}
```

</p>
</details>

---

Tags: _#DJS_ _#MID_

Write polyfill for bind

<details><summary><b>Answer</b></summary>
<p>

```javascript
Function.prototype.bind = function(...args) {
    const self = this;
    const context = args.shift();
    return function(...args2) {
        return self.call(context, ...args, ...args2);
    }
}
```

</p>
</details>

---

Tags: _#DJS_ _#MID_

Write deep copy for value

```javascript
var val = JSON.parse(str);

function deepCopy(val) {
    // your code
}

var val2 = deepCopy(val);
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
function deepCopy(val) {
    const type = typeof val;
    if (type === 'object' && val !== null) {
        if (Array.isArray(val)) {
            return val.map(deepCopy);
        }
        
        // object
        return Object.keys(val).reduce((res, key) => {
            res[key] = deepCopy(val[key]);
            return res;
        }, {})
    }
    
    return val;
}
```

</p>
</details>

---

Tags: _#AL_ _#HARD_

```javascript
/**
У нас есть набор билетов вида:

[
    { from: 'London', to: 'Moscow' },
    { from: 'NY', to: 'London' },
    { from: 'Moscow', to: 'SPb' },
    ...
]

Из этих билетов можно построить единственный, неразрывный маршрут.
Петель и повторов в маршруте нет.

Нужно написать программу, которая возвращает билеты 
в порядке следования по маршруту.
*/

function getRoute(tickets = []) {
    // your code here
}
```

<details><summary><b>Answer</b></summary>
<p>

- You should use graph

</p>
</details>

---

Tags: _#AL_ _#HARD_

```javascript
compress([1, 4, 5, 2, 3, 9, 8, 11, 0]); // '0-5,8-9,11'
compress([1, 4, 3, 2]); // '1-4'
compress([1, 4]); // '1,4'

function compress(list) {
    // your code here
}
```

<details><summary><b>Answer</b></summary>
<p>

- Check code with this data
```javascript
compress([1, 2]); // '1-2'
compress([1, 2, 6]); // '1-2,6'
compress([1, 2, 6, 7]); // '1-2,6-7'
compress([1, 2, 6, 7, 4]); // '1-2,4,6-7'
```
- You should remember about boundary values

</p>
</details>

---

Tags: _#LA_ _#MID_

Put div to center

```html
<style>
.center {
    width: 100px;
    height: 100px;
    background: red;
}
</style>
<body>
    <div class="center"></div>
</body>
```

<details><summary><b>Answer</b></summary>
<p>

- You should use flex
```css
div.center {
  display: flex;
  align-items: center;
  justify-content: center 
}
``` 
- https://www.w3schools.com/css/css_align.asp
- https://www.w3.org/Style/Examples/007/center.html

</p>
</details>

---

Tags: _#LA_ _#NOOB_

What will each line return? Write answer in comments

```html
<div id="root">
    <span id="id1"></span>
    <div id="id2">
        <div id="id3"></div>
    </div>
</div>

<script>
var root = document.getElementById('root');

root.getElementsByTagName('div'); //
root.querySelector('div:first-child'); 
root.querySelectorAll('div')[0]; //
</script>
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
root.getElementsByTagName('div'); // id2, id3
root.querySelector('div:first-child'); //id3 
root.querySelectorAll('div')[0]; // id2
```

</p>
</details>

---

Tags: _#JS_ _#NOOB_

```javascript
function Book() {
    this.name = 'foo';
}

Book.prototype = {
    getName: function() {
        return this.name;
    }
}

var book = new Book();

Book.prototype.getUpperName = function() {
    return this.getName().toUpperCase();
}

console.log(book.getUpperName());
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
console.log(book.getUpperName()); // FOO
```

</p>
</details>

---

Tags: _#JS_ _#MID_

```javascript
typeof (function(){})();

typeof typeof (function(){})();
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
typeof (function(){})(); // 'undefined'

typeof typeof (function(){})(); // 'string'
```

</p>
</details>

---

Tags: _#JS_ _#MID_

```javascript
Promise.resolve(1)
  .then(function (x) { return x + 1; })
  .then(function (x) { throw new Error('My Error'); })
  .catch(function () { return 1; })
  .then(function (x) { return x + 1; })
  .then(function (x) { console.log(x); })
  .catch(console.error)
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
2
```

</p>
</details>

---

Tags: _JS_ _#MID_

```javascript
/**
 * Необходимо написать функцию, которая на вход принимает урл, 
 * асинхронно ходит по этому урлу GET запросом и возвращает данные (json).
 * Для получении данных можно использовать $.get или fetch.
 * Если во время запроса произошла ошибка, то пробовать запросить ещё 5 раз.
 * Если в итоге информацию получить не удалось, вернуть ошибку "Заданный URL недоступен".
 */
function get(url, count = 0) {
  // code here
}

get(url)
 .then(res => console.log(res))
 .catch(err => console.error(err))
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
function get(url, count = 0) {
  return $.get(url).catch(() => {
      if (count++ === 5) {
          throw new Error('Заданный URL недоступен')
      }
      return get(url, count);
  });
}
```

</p>
</details>

---

Tags: _#AL_ _#MID_

```javascript
// Нужно написать функцию, которая определяет, является ли переданная строка палиндромом.
// Примеры палиндромов:

// Казак
// А роза упала на лапу Азора
// Do geese see God?
// Madam, I’m Adam
```

<details><summary><b>Answer</b></summary>
<p>

```javascript
function isP(str) {
    const odd = !(str.length % 2);
    str = str.toLowerCase();
    str = str.replace(/[\S]/g, '');
    for(let i = 0, len = str.length - 1; i < len; i++, len--) {
        if (!odd && i === len) return true;
        if (str[i] !== str[len]) return false;
    }
    
    return true;
}
```

</p>
</details>