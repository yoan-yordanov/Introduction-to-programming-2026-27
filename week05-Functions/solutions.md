# Седмица 5 - Функции - решения

## Задача 1

Започваме с `result = 1` и умножаваме резултата по `number` точно `exponent` пъти. При отрицателна степен връщаме реципрочната стойност. Използваме `double`, за да можем да връщаме и дробни резултати. При степен 0 функцията връща 1.

```cpp
#include <iostream>

double power(double number, int exponent) {
    double result = 1;

    int iterations = exponent;

    if (exponent < 0) {
        iterations = -exponent;
    }

    for (int i = 0; i < iterations; i++) {
        result *= number;
    }

    if (exponent < 0) {
        return 1 / result;
    }

    return result;
}

int main() {
    double number;
    int exponent;

    std::cin >> number >> exponent;

    std::cout << power(number, exponent);

    return 0;
}
```

## Задача 2

За да намерим броя на цифрите, разделяме числото на 10, докато стане 0, като при всяко деление увеличаваме брояча. Отрицателните числа първо превръщаме в положителни, защото иначе няма да влезем в цикъла. Обработваме отделно числото 0, тъй няма да влезнем в цикъла.

```cpp
#include <iostream>

int length(int number) {
    int count = 0;

    if (number == 0) {
        return 1;
    }

    if (number < 0) {
        number = -number;
    }

    while (number > 0) {
        count++;
        number /= 10;
    }

    return count;
}

int main() {
    int number;
    std::cin >> number;

    std::cout << length(number);

    return 0;
}
```

## Задача 3

Използваме функциите `power` от задача 1 и `length` от задача 2. Умножаваме първото число по 10, повдигнато на степен броя на цифрите на второто число. След това прибавяме второто число. Така освобождаваме необходимото място за неговите цифри.

```cpp
#include <iostream>

double power(double number, int exponent) {
    double result = 1;

    int iterations = exponent;

    if (exponent < 0) {
        iterations = -exponent;
    }

    for (int i = 0; i < iterations; i++) {
        result *= number;
    }

    if (exponent < 0) {
        return 1 / result;
    }

    return result;
}

int length(int number) {
    int count = 0;

    if (number == 0) {
        return 1;
    }

    if (number < 0) {
        number = -number;
    }

    while (number > 0) {
        count++;
        number /= 10;
    }

    return count;
}

int concatenate(int first, int second) {
    return first * power(10, length(second)) + second;
}

int main() {
    int first, second;
    std::cin >> first >> second;

    std::cout << concatenate(first, second);

    return 0;
}
```

## Задача 4

Първо преобразуваме десетичното число в двоично. За целта последователно делим на 2 и използваме остатъците, за да изградим двоичния запис. След това обръщаме полученото число чрез `reverseNumber`. Ако първоначалният двоичен запис и обърнатият запис са равни, числото е палиндром.

Използваме `long long` за двоичния запис, защото броя на цифрите на двоичните числа расте бързо и при малко по-големи числа int-a може да overflow-не.

```cpp
#include <iostream>

long long convertToBinary(int number) {
    long long binary = 0;
    long long multiplier = 1;

    while (number > 0) {
        int digit = number % 2;
        binary += digit * multiplier;
        multiplier *= 10;
        number /= 2;
    }

    return binary;
}

long long reverseNumber(long long number) {
    long long reversed = 0;

    while (number > 0) {
        int digit = number % 10;
        reversed = reversed * 10 + digit;
        number /= 10;
    }

    return reversed;
}

bool isBinaryPalindrome(int number) {
    long long binary = convertToBinary(number);

    return binary == reverseNumber(binary);
}

int main() {
    int number;
    std::cin >> number;

    std::cout << std::boolalpha << isBinaryPalindrome(number);

    return 0;
}
```

## Задача 5

Използваме function overloading - дефинираме две функции с еднакво име, но с различни типове на параметрите. Компилаторът избира коя функция да извика според типовете на подадените аргументи. При `int` се извършва целочислено деление, а при `double` резултатът може да има дробна част.

```cpp
#include <iostream>

int divide(int a, int b) {
    return a / b;
}

double divide(double a, double b) {
    return a / b;
}

int main() {
    std::cout << divide(10, 3) << '\n';
    std::cout << divide(10.0, 3.0) << '\n';

    return 0;
}
```

## Задача 6

Съвършено е число, което е равно на сумата на положителните си делители, различни от самото него. Обхождаме всички числа от 1 до `number - 1` и проверяваме кои от тях са делители. Ако остатъкът при деление е 0, добавяме съответното число към сумата. Накрая сравняваме сумата с първоначалното число.

```cpp
#include <iostream>

bool isPerfect(int number) {
    int sum = 0;

    for (int i = 1; i < number; i++) {
        if (number % i == 0) {
            sum += i;
        }
    }

    return sum == number;
}

int main() {
    int number;
    std::cin >> number;

    std::cout << std::boolalpha << isPerfect(number);

    return 0;
}
```

## Задача 7

Използваме функцията `isPerfect` от задача 6. Обхождаме всички числа в интервала `[a, b]` и за всяко проверяваме дали е съвършено. Ако функцията върне `true`, извеждаме числото. Използваме `void`, защото функцията трябва да извежда резултат, а не да връща такъв.

```cpp
#include <iostream>

bool isPerfect(int number) {
    int sum = 0;

    for (int i = 1; i < number; i++) {
        if (number % i == 0) {
            sum += i;
        }
    }

    return sum == number;
}

void printPerfectNumbers(int a, int b) {
    for (int i = a; i <= b; i++) {
        if (isPerfect(i)) {
            std::cout << i << " ";
        }
    }
}

int main() {
    int a, b;
    std::cin >> a >> b;

    printPerfectNumbers(a, b);

    return 0;
}
```

## Задача 8

Обхождаме цифрите на числото отдясно наляво. Ако текущата цифра е различна от тази, която трябва да премахнем, я добавяме към новото число. Използваме `multiplier`, за да определим позицията на всяка добавена цифра. Увеличаваме го само когато добавим цифра, защото пропуснатите цифри не трябва да заемат позиция в резултата.

```cpp
#include <iostream>

int removeDigit(int number, int digit) {
    int result = 0;
    int multiplier = 1;

    while (number > 0) {
        int currentDigit = number % 10;

        if (currentDigit != digit) {
            result += currentDigit * multiplier;
            multiplier *= 10;
        }

        number /= 10;
    }

    return result;
}

int main() {
    int number, digit;
    std::cin >> number >> digit;

    std::cout << removeDigit(number, digit);

    return 0;
}
```

## Задача 9

Проверяваме всяка цифра от 0 до 9, но премахваме само тези, които действително се срещат в числото. За целта използваме допълнителна функция `containsDigit`. За всяка срещаща се цифра извикваме `removeDigit` от задача 8 и сравняваме получения резултат с досегашния най-голям. Накрая връщаме най-голямото получено число.

```cpp
#include <iostream>

int removeDigit(int number, int digit) {
    int result = 0;
    int multiplier = 1;

    while (number > 0) {
        int currentDigit = number % 10;

        if (currentDigit != digit) {
            result += currentDigit * multiplier;
            multiplier *= 10;
        }

        number /= 10;
    }

    return result;
}

bool containsDigit(int number, int digit) {
    while (number > 0) {
        if (number % 10 == digit) {
            return true;
        }

        number /= 10;
    }

    return false;
}

int largestAfterRemovingDigit(int number) {
    int largest = 0;

    for (int digit = 0; digit <= 9; digit++) {
        if (containsDigit(number, digit)) {
            int result = removeDigit(number, digit);

            if (result > largest) {
                largest = result;
            }
        }
    }

    return largest;
}

int main() {
    int number;
    std::cin >> number;

    std::cout << largestAfterRemovingDigit(number);

    return 0;
}
```

## Задача 10

Използваме алгоритъма на Евклид за намиране на НОД на две числа. За да намерим НОД на повече числа, прилагаме алгоритъма последователно: `НОД(a, b, c) = НОД(НОД(a, b), c)`. Започваме с `result = 0`, защото `НОД(0, a) = a`.

```cpp
#include <iostream>

int gcd(int a, int b) {
    while (b != 0) {
        int remainder = a % b;
        a = b;
        b = remainder;
    }

    return a;
}

int main() {
    int number;
    int result = 0;

    std::cin >> number;

    while (number != -1) {
        result = gcd(result, number);

        std::cin >> number;
    }

    std::cout << result;

    return 0;
}
```