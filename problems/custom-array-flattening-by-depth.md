[/ Меню](https://github.com/samatakaya1/Interview-material/blob/main/README.md)   [/ Список задач](https://github.com/samatakaya1/Interview-material/blob/main/problems/problems.md)
---
# Задача "Выровнять глубоко вложенный массив"


### Постановка

Написать функцию, которая принимает глубоко вложенный массив **arr** и разворачивает его до заданного уровня **n** вложенности.

>**arr** : массив, который может содержать как элементы, так и другие массивы (глубоко вложенные).

>**n** : целое число, указывающее уровень вложенности, до которого необходимо развернуть массив. Например, если n = 1, то функция должна развернуть только первый уровень вложенности, если n = 2, то два уровня и так далее.


<details>
<summary>Ограничения</summary>
<br/>

> - Глубина вложенности массива может достигать **1000** уровней.
> - Значение **n** всегда будет неотрицательным целым числом.
> - Массив может содержать любые типы данных (числа, строки, объекты, другие массивы и т.д.).
> - Запрещается использовать встроенный метод **Array.prototype.flat()**.


</details>

---

### Пример
> Если **arr** = [1, [2, [3, [4]]]] и **n** = 2, то результат должен быть [1, 2, 3, [4]].

---

### Решения


###### 1.Рекурсивный подход

Алгоритм:
- Для каждого элемента массива проверяем, является ли он вложенным массивом (с помощью Array.isArray()).
- Если элемент является массивом и текущая глубина (n) больше нуля, вызываем функцию flat рекурсивно с этим элементом и глубиной на единицу меньше (n - 1).
- Развёрнутый массив добавляем в результирующий массив.


Код: 

```js
var flat = function(arr, n) {
    // Базовый случай: если глубина 0, возвращаем исходный массив
    if (n === 0) return arr;

    // Результирующий массив
    const result = [];

    // Обходим каждый элемент в массиве
    for (const item of arr) {
        // Если элемент - массив и глубина больше 0
        if (Array.isArray(item) && n > 0) {
            // Разворачиваем этот элемент с глубиной n-1 и добавляем его элементы в результат
            result.push(...flat(item, n - 1));
        } else {
            // Если элемент не массив, добавляем его в результат напрямую
            result.push(item);
        }
    }

    return result;
};

```

Временная и пространственная сложность:

 - Временная сложность: В худшем случае, если все элементы вложены максимально глубоко, время работы будет **O(n)**, где **n** — общее количество элементов во всех вложенных массивах.
- Пространственная сложность: **O(m + n)** для рекурсивного решения (включая стек вызовов), где **m** — для хранения результирующего массива, а **n** — для хранения стека вызовов в случае максимальной глубины вложенности.

---

###### 2. Итеративный подход (альтернатива)

> Вместо рекурсии можно использовать стек для имитации глубины вызовов. В этом случае элементы будут извлекаться из стека, и если они являются массивами, будут добавляться обратно с уменьшенной глубиной.


Алгоритм: 

- Стек инициализируется объектом, содержащим исходный массив и глубину n.


- Пока стек не пуст, мы извлекаем массив и текущую глубину из вершины стека.

- Если элемент — массив и глубина больше 0, помещаем его обратно в стек с уменьшенной глубиной.

- Если элемент не является массивом или глубина достигла 0, добавляем его в результирующий массив.

- Элементы добавляются в результирующий массив в порядке их обхода.

- После того как все элементы будут обработаны, стек станет пустым, и мы вернём сформированный результирующий массив.



Код:

```js
var flat = function(arr, n) {
    // Инициализируем стек начальным массивом и текущей глубиной n
    const stack = [{ array: arr, depth: n }];
    const result = [];

    // Пока стек не пуст
    while (stack.length > 0) {
        // Извлекаем последний элемент из стека
        const { array, depth } = stack.pop();

        // Используем цикл for...of для обхода элементов массива
        for (const item of array) {
            // Если элемент - массив и глубина ещё не достигла 0
            if (Array.isArray(item) && depth > 0) {
                // Добавляем его в стек с уменьшенной глубиной
                stack.push({ array: item, depth: depth - 1 });
            } else {
                // Если элемент не массив или глубина равна 0, добавляем его в результат
                result.push(item);
            }
        }
    }

    return result;
};
```

Временная и пространственная сложность:

- Временная сложность: **O(n)**, где **n** — общее количество элементов в массиве.
- Пространственная сложность: В худшем случае — **O(n)** из-за возможного максимального размера стека.

---
[<- К списку задач](https://github.com/samatakaya1/Interview-material/blob/main/problems/problems.md)
