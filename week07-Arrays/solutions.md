# Седмица 6 – Масиви

## Задача 1

Размерът на масив от цели числа `size` е известен. Въведете толкова числа от стандартния вход, изведете елементите и сумата им.

### Решение

```cpp
#include <iostream>

int main() {
    const unsigned SIZE = 5;
    int arr[SIZE];

    int sum = 0;

    for (unsigned i = 0; i < SIZE; ++i) {
        std::cin >> arr[i];
        sum += arr[i];
    }

    std::cout << "Elements: ";

    for (unsigned i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << ' ';
    }

    std::cout << "\nSum: " << sum;

    return 0;
}
```

**Обяснение:**

Въвеждаме 5 числа в масива и едновременно пресмятаме сумата им. След това обхождаме масива повторно, за да изведем елементите.

---

## Задача 2

Масив е инициализиран с цели числа. В константа запазете размера му и проверете дали произведението на първия и последния елемент е равно на сумата на останалите елементи.

### Решение

```cpp
#include <iostream>

int main() {
    int arr[] = { 2, 3, 4, 5, 6 };

    const unsigned SIZE = sizeof(arr) / sizeof(arr[0]);

    int product = arr[0] * arr[SIZE - 1];
    int sum = 0;

    for (unsigned i = 1; i < SIZE - 1; ++i) {
        sum += arr[i];
    }

    if (product == sum) {
        std::cout << "Equal";
    }
    else {
        std::cout << "Not equal";
    }

    return 0;
}
```

**Обяснение:**

- `sizeof(arr)` връща общия размер на масива в байтове.
- `sizeof(arr[0])` връща размера на един елемент.
- Делението им дава броя на елементите.

Пресмятаме произведението на първия и последния елемент и сумата на всички елементи между тях.

---

## Задача 3

Да се създаде масив от 5 естествени числа, въведени от терминала. Елементите на четните позиции се умножават по 2, а на нечетните се делят на 2. Изведете променения масив.

### Решение

```cpp
#include <iostream>

int main() {
    const unsigned SIZE = 5;
    int arr[SIZE];

    for (unsigned i = 0; i < SIZE; ++i) {
        std::cin >> arr[i];
    }

    for (unsigned i = 0; i < SIZE; ++i) {
        if (i % 2 == 0) {
            arr[i] *= 2;
        }
        else {
            arr[i] /= 2;
        }
    }

    for (unsigned i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << ' ';
    }

    return 0;
}
```

**Обяснение:**

Тук гледаме индексите на елементите, които започват от 0:

- При четен индекс (`i % 2 == 0`) умножаваме елемента по 2.
- При нечетен индекс (`i % 2 != 0`) делим елемента на 2.

---

## Задача 4

Напишете функция, която по подаден масив от цели числа и неговия размер, по-голям от 0, връща индекса на най-малкото число. Ако най-малкото число се среща повече от веднъж, да се върне индексът на първото срещане.

### Решение

```cpp
#include <iostream>

int getMinIndex(const int arr[], unsigned size) {
    unsigned minIndex = 0;

    for (unsigned i = 1; i < size; ++i) {
        if (arr[i] < arr[minIndex]) {
            minIndex = i;
        }
    }

    return minIndex;
}

int main() {
    const unsigned SIZE = 6;
    int arr[SIZE] = { 8, 3, 5, 2, 7, 2 };

    std::cout << getMinIndex(arr, SIZE);

    return 0;
}
```

**Обяснение:**

Първоначално приемаме, че най-малкият елемент е на индекс 0. Обхождаме останалите елементи и при откриване на по-малък запазваме индекса му.

Използваме `<`, а не `<=`, за да запазим индекса на първото срещане на най-малкия елемент.

---

## Задача 5

Напишете функция, която по подаден масив от цели числа, неговия размер и цяло число връща индекса на неговото първо срещане в масива. Ако го няма в масива, се връща -1.

### Решение

```cpp
#include <iostream>

int findElement(const int arr[], unsigned size, int number) {
    for (unsigned i = 0; i < size; ++i) {
        if (arr[i] == number) {
            return i;
        }
    }

    return -1;
}

int main() {
    const unsigned SIZE = 6;
    int arr[SIZE] = { 4, 7, 2, 7, 9, 1 };

    std::cout << findElement(arr, SIZE, 7);

    return 0;
}
```

**Обяснение:**

Обхождаме масива от началото. При първото съвпадение връщаме индекса. Ако числото не бъде намерено, връщаме `-1`.

### Бонус – индекс на последното срещане

```cpp
int findLastElement(const int arr[], unsigned size, int number) {
    for (int i = size - 1; i >= 0; --i) {
        if (arr[i] == number) {
            return i;
        }
    }

    return -1;
}
```

Обхождаме масива отзад напред, затова първото намерено съвпадение е последното срещане в оригиналния масив.

---

## Задача 6

Напишете функция, която премахва последното срещане на най-голямото число в масив. Броят елементи да се намали.

### Решение

```cpp
#include <iostream>

void removeLastMax(int arr[], unsigned& size) {
    unsigned maxIndex = 0;

    for (unsigned i = 1; i < size; ++i) {
        if (arr[i] >= arr[maxIndex]) {
            maxIndex = i;
        }
    }

    for (unsigned i = maxIndex; i < size - 1; ++i) {
        arr[i] = arr[i + 1];
    }

    --size;
}

int main() {
    const unsigned MAX_SIZE = 10;
    int arr[MAX_SIZE] = { 1, 3, 9, 4, 9, 7, 1 };
    unsigned size = 7;

    removeLastMax(arr, size);

    for (unsigned i = 0; i < size; ++i) {
        std::cout << arr[i] << ' ';
    }

    return 0;
}
```

**Обяснение:**

Първо намираме индекса на последното срещане на максималния елемент. Използваме `>=`, за да актуализираме индекса и при равни максимални стойности.

След това изместваме всички елементи след него с една позиция наляво и намаляваме размера.

Подаваме `size` с референция (`unsigned&`), за да се промени и в `main()`.

---

## Задача 7

Напишете програма, която проверява дали елементите на масив от цели числа се повтарят, ако:

1. Елементите са сортирани в низходящ ред.
2. Елементите нямат наредба.

### Първи случай – масивът е сортиран в низходящ ред

```cpp
#include <iostream>

bool hasDuplicatesSorted(const int arr[], unsigned size) {
    for (unsigned i = 0; i < size - 1; ++i) {
        if (arr[i] == arr[i + 1]) {
            return true;
        }
    }

    return false;
}

int main() {
    const unsigned SIZE = 6;
    int arr[SIZE] = { 9, 7, 7, 5, 3, 1 };

    if (hasDuplicatesSorted(arr, SIZE)) {
        std::cout << "There are duplicates";
    }
    else {
        std::cout << "There are no duplicates";
    }

    return 0;
}
```

### Втори случай – масивът няма наредба

```cpp
#include <iostream>

bool hasDuplicates(const int arr[], unsigned size) {
    for (unsigned i = 0; i < size; ++i) {
        for (unsigned j = i + 1; j < size; ++j) {
            if (arr[i] == arr[j]) {
                return true;
            }
        }
    }

    return false;
}

int main() {
    const unsigned SIZE = 6;
    int arr[SIZE] = { 4, 2, 8, 3, 2, 9 };

    if (hasDuplicates(arr, SIZE)) {
        std::cout << "There are duplicates";
    }
    else {
        std::cout << "There are no duplicates";
    }

    return 0;
}
```

**Обяснение:**

В първия случай е достатъчно да сравняваме съседните елементи, защото масивът е сортиран.

Във втория случай използваме два вложени цикъла, за да сравним всеки елемент с всички следващи.

---

## Задача 8

По дадена пермутация на числата от 1 до 5 да се пресметне броят на инверсиите в нея.

### Решение

```cpp
#include <iostream>

int countInversions(const int arr[], unsigned size) {
    int inversions = 0;

    for (unsigned i = 0; i < size; ++i) {
        for (unsigned j = i + 1; j < size; ++j) {
            if (arr[i] > arr[j]) {
                ++inversions;
            }
        }
    }

    return inversions;
}

int main() {
    const unsigned SIZE = 5;
    int arr[SIZE];

    for (unsigned i = 0; i < SIZE; ++i) {
        std::cin >> arr[i];
    }

    std::cout << countInversions(arr, SIZE);

    return 0;
}
```

**Обяснение:**

Изнасяме логиката за намиране на инверсиите във функцията `countInversions()`.

Използваме два вложени цикъла, за да проверим всички двойки елементи.

Ако по-голямото число се намира преди по-малкото (`arr[i] > arr[j]`), увеличаваме брояча на инверсиите.

Пример:

```text
1 3 5 4 2
```

Инверсиите са:

- 3 и 2
- 5 и 4
- 5 и 2
- 4 и 2

Следователно резултатът е `4`.

---

## Задача 9

Подават се два масива `x` и `y` от цели числа с размер `n`, като `(x[i], y[i])` са точки в декартова координатна система.

Да се изведе най-малкото евклидово разстояние между кои да е две точки и координатите на тези две точки.

### Решение

```cpp
#include <iostream>
#include <cmath>

int main() {
    const unsigned MAX_SIZE = 100;

    int x[MAX_SIZE];
    int y[MAX_SIZE];

    unsigned n;
    std::cin >> n;

    for (unsigned i = 0; i < n; ++i) {
        std::cin >> x[i] >> y[i];
    }

    double minDistance = -1;
    unsigned first = 0;
    unsigned second = 0;

    for (unsigned i = 0; i < n; ++i) {
        for (unsigned j = i + 1; j < n; ++j) {
            double dx = x[i] - x[j];
            double dy = y[i] - y[j];

            double distance = std::sqrt(dx * dx + dy * dy);

            if (minDistance == -1 || distance < minDistance) {
                minDistance = distance;
                first = i;
                second = j;
            }
        }
    }

    std::cout << "Minimum distance: " << minDistance << '\n';

    std::cout << "First point: ("
              << x[first] << ", " << y[first] << ")\n";

    std::cout << "Second point: ("
              << x[second] << ", " << y[second] << ")\n";

    return 0;
}
```

**Обяснение:**

Използваме формулата за евклидово разстояние:

d = √((xᵢ − xⱼ)² + (yᵢ − yⱼ)²)

Двата масива съхраняват координатите на точките:
- `x[i]` – абсциса;
- `y[i]` – ордината.

С два вложени цикъла проверяваме разстоянието между всяка двойка точки.

Запазваме най-малкото разстояние и индексите на двете точки.

Започваме вътрешния цикъл от `i + 1`, за да не сравняваме точката със самата нея и да не проверяваме една двойка два пъти.

Приемаме, че `n` е поне 2 и не надвишава 100.

---

## Задача 10

Напишете функция, която вмъква число в сортиран във възходящ ред масив, без да нарушава наредбата му.

### Решение

```cpp
#include <iostream>

unsigned getIndexToInsertInSortedArray(
    const int arr[], unsigned size, int element) {

    unsigned i = 0;

    while (i < size && arr[i] < element) {
        ++i;
    }

    return i;
}

void insertElementInSortedArray(
    int arr[], unsigned& size, int element) {

    unsigned index = getIndexToInsertInSortedArray(
        arr, size, element
    );

    for (unsigned i = size; i > index; --i) {
        arr[i] = arr[i - 1];
    }

    arr[index] = element;
    ++size;
}

int main() {
    const unsigned MAX_SIZE = 10;

    int arr[MAX_SIZE] = { 1, 2, 3, 4, 5, 6 };
    unsigned size = 6;

    int element;
    std::cin >> element;

    insertElementInSortedArray(arr, size, element);

    for (unsigned i = 0; i < size; ++i) {
        std::cout << arr[i] << ' ';
    }

    return 0;
}
```

**Обяснение:**

Използваме две функции.

**1. `getIndexToInsertInSortedArray()`**

Намира индекса, на който трябва да поставим новия елемент.

Обхождаме масива, докато намерим първия елемент, който е по-голям или равен на числото, което искаме да добавим.

Ако всички елементи са по-малки, връщаме `size`, което означава, че добавяме числото в края.

**2. `insertElementInSortedArray()`**

След като знаем индекса, трябва да освободим място за новия елемент.

```cpp
for (unsigned i = size; i > index; --i) {
    arr[i] = arr[i - 1];
}
```

Изместваме елементите надясно, като започваме от края, за да не презапишем стойности, които все още са ни необходими.

След това записваме новото число и увеличаваме размера.

---

## Задача 11

Напишете програма, която приема от конзолата естествено число `num`. Принтирайте сумата на уникалните цифри – тези, които се срещат само веднъж.

### Решение

```cpp
#include <iostream>

int main() {
    unsigned long long num;
    std::cin >> num;

    unsigned counts[10] = {};

    if (num == 0) {
        counts[0] = 1;
    }

    while (num > 0) {
        unsigned digit = num % 10;
        ++counts[digit];
        num /= 10;
    }

    unsigned sum = 0;

    for (unsigned i = 0; i < 10; ++i) {
        if (counts[i] == 1) {
            sum += i;
        }
    }

    std::cout << sum;

    return 0;
}
```

**Обяснение:**

Създаваме помощен масив от 10 елемента и го зануляваме:

```cpp
unsigned counts[10] = {};
```

Всеки индекс отговаря на съответната цифра от 0 до 9. В него пазим колко пъти се среща цифрата.

Използваме `% 10`, за да вземем последната цифра, и `/ 10`, за да я премахнем от числото.

Например при числото `122345` получаваме:

| Цифра | Брой срещания |
|---|---:|
| 1 | 1 |
| 2 | 2 |
| 3 | 1 |
| 4 | 1 |
| 5 | 1 |

Накрая събираме цифрите, които се срещат точно веднъж:

\[
1+3+4+5=13
\]

---

## Задача 12

Напишете функция, която проверява дали числото, получено при конкатенация на елементите на масива, образува палиндром.

### Вариант 1 – с два брояча

```cpp
#include <iostream>

bool isPalindrome(const int arr[], unsigned size) {
    unsigned left = 0;
    unsigned right = size - 1;

    while (left < right) {
        if (arr[left] != arr[right]) {
            return false;
        }

        ++left;
        --right;
    }

    return true;
}

int main() {
    const unsigned SIZE = 5;
    int arr[SIZE] = { 1, 2, 3, 2, 1 };

    if (isPalindrome(arr, SIZE)) {
        std::cout << "Palindrome";
    }
    else {
        std::cout << "Not palindrome";
    }

    return 0;
}
```

**Обяснение:**

Използваме два брояча:
- `left` започва от първия елемент.
- `right` започва от последния елемент.

Сравняваме елементите и постепенно придвижваме броячите един към друг.

Ако намерим различни елементи, връщаме `false`. Ако стигнем до средата, връщаме `true`.

### Вариант 2 – с един брояч

```cpp
#include <iostream>

bool isPalindrome(const int arr[], unsigned size) {
    for (unsigned i = 0; i < size / 2; ++i) {
        if (arr[i] != arr[size - 1 - i]) {
            return false;
        }
    }

    return true;
}

int main() {
    const unsigned SIZE = 6;
    int arr[SIZE] = { 1, 2, 3, 3, 2, 1 };

    if (isPalindrome(arr, SIZE)) {
        std::cout << "Palindrome";
    }
    else {
        std::cout << "Not palindrome";
    }

    return 0;
}
```

**Обяснение:**

Тук използваме само един брояч `i`.

Сравняваме:

```cpp
arr[i] == arr[size - 1 - i]
```

Така намираме съответния елемент от края на масива, без да е необходим втори брояч.

Цикълът се изпълнява само до `size / 2`, защото не е необходимо да проверяваме елементите повторно.

---

## Задача 13

Да се дефинират с инициализация два масива от цели числа, да се провери дали са сортирани във възходящ ред и да се слеят в един сортиран масив.

### Решение

```cpp
#include <iostream>

bool isSorted(const int arr[], unsigned size) {
    for (unsigned i = 0; i < size - 1; ++i) {
        if (arr[i] > arr[i + 1]) {
            return false;
        }
    }

    return true;
}

void mergeSortedArrays(
    const int left[], unsigned leftSize,
    const int right[], unsigned rightSize,
    int merged[]) {

    unsigned i = 0;
    unsigned j = 0;
    unsigned k = 0;

    while (i < leftSize && j < rightSize) {
        if (left[i] <= right[j]) {
            merged[k] = left[i];
            ++i;
        }
        else {
            merged[k] = right[j];
            ++j;
        }

        ++k;
    }

    while (i < leftSize) {
        merged[k] = left[i];
        ++i;
        ++k;
    }

    while (j < rightSize) {
        merged[k] = right[j];
        ++j;
        ++k;
    }
}

int main() {
    const unsigned SIZE_ARR1 = 5;
    int arr1[SIZE_ARR1] = { 1, 1, 5, 7, 9 };

    const unsigned SIZE_ARR2 = 7;
    int arr2[SIZE_ARR2] = { 2, 3, 5, 8, 11, 12, 13 };

    if (!isSorted(arr1, SIZE_ARR1) ||
        !isSorted(arr2, SIZE_ARR2)) {

        std::cout << "Arrays are not sorted";
        return 0;
    }

    const unsigned MERGED_SIZE = SIZE_ARR1 + SIZE_ARR2;
    int merged[MERGED_SIZE];

    mergeSortedArrays(
        arr1, SIZE_ARR1,
        arr2, SIZE_ARR2,
        merged
    );

    for (unsigned i = 0; i < MERGED_SIZE; ++i) {
        std::cout << merged[i] << ' ';
    }

    return 0;
}
```

**Обяснение:**

Задачата е разделена на две основни функции.

**1. `isSorted()`**

Проверява дали масивът е сортиран във възходящ ред.

Сравняваме всеки елемент със следващия. Ако намерим елемент, който е по-голям от следващия, връщаме `false`.

Използваме `>`, а не `>=`, защото повторенията са позволени.

**2. `mergeSortedArrays()`**

Използваме три брояча:

- `i` – текущ индекс в първия масив.
- `j` – текущ индекс във втория масив.
- `k` – текущ индекс в новия масив.

Сравняваме текущите елементи от двата масива и записваме по-малкия в `merged`.

Когато единият масив свърши, копираме останалите елементи от другия с помощта на двата последни цикъла.

Резултатът е:

```text
1 1 2 3 5 5 7 8 9 11 12 13
```