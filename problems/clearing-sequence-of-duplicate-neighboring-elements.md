


[/ Меню](https://github.com/samatakaya1/Interview-material/blob/main/README.md)   [/ Список задач](https://github.com/samatakaya1/Interview-material/blob/main/problems/problems.md)
---
# Задача "Очистка последовательности от повторяющихся соседних элементов"


## Постановка 📖

Необходимо реализовать функцию, которая принимает на вход последовательность элементов (строка или массив) и возвращает новый массив, в котором:

1. Соседние одинаковые элементы удаляются.
2. Порядок оставшихся элементов сохраняется.

#### Входные данные:
- Последовательность элементов в виде строки или массива.

#### Выходные данные:
- Массив, где все повторяющиеся подряд элементы удалены, но первоначальный порядок элементов сохранён.

#### Примеры

```typescript
foo('AAAABBBCCDAABBB')  // ['A', 'B', 'C', 'D', 'A', 'B']
foo('ABBCcAD')          // ['A', 'B', 'C', 'c', 'A', 'D']
foo([1, 2, 2, 3, 3])    // [1, 2, 3]
```

## Решения

### Вариант 1: Через цикл

Этот вариант использует цикл для последовательного сравнения каждого элемента с предыдущим и добавления его в результат, если они не совпадают.

```typescript
function foo<T>(sequence: T[]): T[] {
    if (sequence.length === 0) return [];

    const result: T[] = [sequence[0]];  // Начинаем с первого элемента

    for (let i = 1; i < sequence.length; i++) {
        if (sequence[i] !== sequence[i - 1]) {
            result.push(sequence[i]);  // Добавляем только если элемент отличается от предыдущего
        }
    }

    return result;
}

// Пример использования:
console.log(foo(['A', 'A', 'A', 'B', 'B', 'C', 'C', 'D', 'A', 'A', 'B', 'B', 'B'])); // ['A', 'B', 'C', 'D', 'A', 'B']
console.log(foo([1, 2, 2, 3, 3])); // [1, 2, 3]
```

#### Сложность:
- **Время**: \( O(n) \), где \( n \) — длина последовательности, так как нужно пройти по каждому элементу один раз.
- **Память**: \( O(n) \), поскольку нам нужно сохранить все элементы в массиве `result`.


### Вариант 2: Через метод `reduce`

Этот вариант использует метод массива `reduce`, чтобы аккумулировать элементы и удалять соседние дубликаты.

```typescript
function foo<T>(sequence: T[]): T[] {
    return sequence.reduce((acc: T[], curr: T) => {
        if (acc.length === 0 || acc[acc.length - 1] !== curr) {
            acc.push(curr);  // Добавляем элемент, если он не равен последнему в аккумуляторе
        }
        return acc;
    }, []);
}

// Пример использования:
console.log(foo(['A', 'A', 'B', 'C', 'C', 'D', 'A', 'B', 'B'])); // ['A', 'B', 'C', 'D', 'A', 'B']
console.log(foo([1, 1, 2, 3, 3])); // [1, 2, 3]
```

#### Сложность:
- **Время**: \( O(n) \), где \( n \) — длина последовательности, так как метод `reduce` проходит по каждому элементу.
- **Память**: \( O(n) \), так как в аккумуляторе хранится результат.

### Общий вывод:

Все предложенные решения имеют одинаковую временную и пространственную сложность:
- **Время**: \( O(n) \), где \( n \) — длина входной последовательности.
- **Память**: \( O(n) \), поскольку результат (массив без дубликатов) занимает столько же места, сколько и исходная последовательность.

---
[<- К списку задач](https://github.com/samatakaya1/Interview-material/blob/main/problems/problems.md)
