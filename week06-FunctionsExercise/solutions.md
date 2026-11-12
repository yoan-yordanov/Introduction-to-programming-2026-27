# Седмица 6 - Упражнение върху функции - Решения

## Задача 1

```c++
#include <iostream>

bool isPrime(unsigned number) {
    if (number <= 1) return false;
    for (unsigned i = 2; i * i <= number; ++i) {
        if (number % i == 0) {
            return false;
        }
    }
    return true;
}

int main() {
    unsigned n;
    std::cin >> n;
    unsigned currNumber = 1;
    while (n > 0) {
        for (unsigned i = 0; i < currNumber && n > 0; ++i) {
            if (currNumber % 2 == 0 && currNumber % 5 == 0) {
                std::cout << "^ ";
            }
            else if (currNumber % 2 == 0) {
                std::cout << "* ";
            }
            else if (currNumber % 5 == 0) {
                std::cout << "$ ";
            }
            else if (isPrime(currNumber)) {
                std::cout << currNumber << ' ';
            }
            else {
                std::cout << "? ";
            }
            --n;
        }
        ++currNumber;
    }
    return 0;
}
```

Да проверим `n > 0` в условието на `for` е съществено. Проверете защо за `n = 5` без тази проверка попадаме в безкраен цикъл.

## Задача 2

```c++
#include <iostream>

int main() {
    double leftA; 
    double rightA;
    double leftB;
    double rightB;
    double number;
    std::cin >> leftA >> rightA;
    std::cin >> leftB >> rightB;
    std::cin >> number;

    bool isInSetA = leftA <= number && number <= rightA;
    bool isInSetB = leftB <= number && number <= rightB;

    bool isInUnion = isInSetA || isInSetB;
    bool isInInters = isInSetA && isInSetB;
    bool isInDiff = isInSetA && !isInSetB;
    bool isInOnlyOneSet = isInSetA && !isInSetB || !isInSetA && isInSetB;
    // bool isInOnlyOneSet = (isInSetA || isInSetB) && !(isInSetA && isInSetB);

    std::cout << "Is in union: " <<  (isInUnion ? "true" : "false") << '\n';
    std::cout << "Is in intersection: " << (isInInters ? "true" : "false") << '\n';
    std::cout << "Is in difference: " <<  (isInDiff ? "true" : "false") << '\n';
    std::cout << "Is in only one set: " << (isInOnlyOneSet ? "true" : "false") << '\n';
    return 0;
}
```

За упражнение: Опитайте да решите задачата, като дефинирате функция, която проверява дали число е елемент на множество. След това изразете обединение, сечение и разлика чрез тази функция. Как `isInOnlyOneSet` може да се направи чрез разлика?

## Задача 3

```c++
#include <iostream>

bool isCountOfOnesAndZeroesInBinaryEqual(unsigned short decimalNumber) {
    unsigned countZeros = 0;
    unsigned countOnes = 0;
    if (decimalNumber == 0) {
        countZeros = 1;
    }
    while (decimalNumber > 0) {
        if (decimalNumber % 2 == 0) 
            ++countZeros;
        else 
            ++countOnes;
        decimalNumber /= 2;
    }
    return countZeros == countOnes;
}

int main() {
    int number;
    std::cin >> number;
    if (number < 0 || number > 255) { // validate input data
        std::cout << "enter number between 0 and 255\n";
        return 1;
    }
    std::cout << (isCountOfOnesAndZeroesInBinaryEqual(number) ? "true" : "false") << '\n';
    return 0;
}
```
Избира се подходящ числов тип `int` за `number`, който побира и отрицателни числа, с цел да валидираме входа. Ако изберем `unsigned`, то например отрицателното число -1 ще се съхрани като 4294967295 - overflow. След като се уверим, че числото е между 0 и 255, типът на параметъра във функцията може да бъде `unsigned short` - 2B.

Прилича на задачата за превръщане на десетично в двоично, но ни трябва само броят на нулите и единиците - няма нужда да конструираме числото в явен вид.

## Задача 4

```c++
#include <iostream>

unsigned long long convertToZigZag(unsigned long long number) {
    int cnt1 = 0, cnt2 = 0, cnt3 = 0, cnt4 = 0, cnt5 = 0;
    while (number > 0) {
        int digit = number % 10;
        switch (digit) {
            case 1: ++cnt1; break;
            case 2: ++cnt2; break;
            case 3: ++cnt3; break;
            case 4: ++cnt4; break;
            case 5: ++cnt5; break;
            default: return 0; // invalid digit
        }
        number /= 10;
    }
    if (cnt1 == 0 || cnt2 == 0 || cnt3 == 0 || cnt4 == 0 || cnt5 == 0) { // някоя от цифрите не се среща нито веднъж
        return 0;
    }
    unsigned long long res = 0;
    unsigned long long coeff = 1;
    for (int i = 0; i < cnt3; ++i) {
        res += coeff * 3;
        coeff *= 10;
    }
    for (int i = 0; i < cnt4; ++i) {
        res += coeff * 4;
        coeff *= 10;
    }
    for (int i = 0; i < cnt2; ++i) {
        res += coeff * 2;
        coeff *= 10;
    }
    for (int i = 0; i < cnt5; ++i) {
        res += coeff * 5;
        coeff *= 10;
    }
    for (int i = 0; i < cnt1; ++i) {
        res += coeff;
        coeff *= 10;
    }
    return res;
}

int main() {
    unsigned long long number;
    std::cin >> number;
    std::cout << "zig-zag: " << convertToZigZag(number) << '\n';
    return 0;
}
```

Числовият тип, който може да събере 64 битово естествено число, е `unsigned long long`. Не се изисква валидация на входа, затова приемаме, че ще се въведе действително положително число и няма да настъпи overflow.


За всяка цифра от 1 до 5 съхраняваме в променлива броя на срещанията в числото. След това в правилния ред добавяме всяка цифра толкова пъти колкото се среща.


Забележете, че `res` и `coeff` също са от тип `unsigned long long`, за да съхранят достатъчно големи естествени числа.

