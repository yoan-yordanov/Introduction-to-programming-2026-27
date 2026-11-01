# Седмица 4 - Решения на задачите

В горния десен ъгъл на това readme има бутон outline (три точки и три черти). Оттам бързо ще намерите съответната задача.

## Задача1

```c++
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= i; ++j) {
            std::cout << j << ' ';
        }
        std::cout << '\n';
    }
    return 0;
}
```

## Задача2

```c++
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (i > 0 && i < n - 1 && j > 0 && j < n - 1) {
                std::cout << ' ';
                continue;
            }
            std::cout << '*';
        }
        std::cout << '\n';
    }
    return 0;
}
```

## Задача3

```c++
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    unsigned num1 = 0;
    unsigned num2 = 1;
    if (n == 1) {
        std::cout << num1;
        return 0;
    }
    std::cout << num1 << ' ' << num2 << ' ';
    unsigned res = 0;
    for (int i = 0; i < n - 2; ++i) {
        res = num1 + num2;
        std::cout << res << ' ';
        num1 = num2;
        num2 = res;
    }
    return 0;
}
```

## Задача4

```c++
#include <iostream>

int main() {
    unsigned a, b;
    std::cin >> a >> b;
    if (a == 0 && b == 0) {
        std::cout << "0 and 0 don't have GCD";
        return 1;
    }
    unsigned remainder;
    while (b > 0) {
        remainder = a % b;
        a = b;
        b = remainder;
    }
    std::cout << "GCD:" << a;
    return 0;
}
```

## Задача 5

Пробвайте да решите първо задача 9.

```c++
#include <iostream>

int main() {
    unsigned num;
    std::cin >> num;
    if (num == 0 || num == 1) {
        std::cout << "0 and 1 don't havе prime factorization";
        return 0;
    }
    for (int i = 2; num > 1 && i <= num; ++i) {
        int counter = 0;
        while (num % i == 0) {
            ++counter;
            num /= i;
        }
        if (counter > 0) {
            std::cout << i << '^' << counter << ' ';
            if (num > 1) { // да извежда *, ако има още делители
                std::cout << "* ";
            }
        } 
    }
    return 0;
}
```
Всяко число `i` от 2 до `num` проверяваме колко пъти дели `num` и съответно разделяме толкова на брой пъти `num`. Според кода съставно число не участва в разлагането, защото неговите прости делители вече са включени на предходни итерации. Например числото 12: 6 е делител, но 2 и 3 са обработени преди 6. Каква оптимизация се постига с проверката в условието в if - `num > 1`?

## Задача 6

```c++
#include <iostream>
#include <cmath>

int main() {
    int num;
    std::cin >> num;
    num = std::abs(num);
    bool areDifferentDigits = true;
    for (int i = 0; i < 10; ++i) {
        int counter = 0;
        int temp = num;
        while (temp > 0) {
            int digit = temp % 10;
            if (digit == i) {
                ++counter;
            }
            temp /= 10;
        }
        if (counter > 1) {
            areDifferentDigits = false;
            break;
        }
    }
    std::cout << (areDifferentDigits ? "diff" : "not diff");
    return 0;
}
```

За всяка цифра от 0 до 9 проверяваме колко пъти се среща в записа на `num`. Как може да се промени кодът, така че да не се използва break и програма отново да завърши по-рано?

## Задача 7

```c++
int main() {
    unsigned start, end;
    std::cin >> start >> end;
    
    for (unsigned i = start; i <= end; ++i) {
        unsigned currNum = i;
        unsigned newNum = 0;
        unsigned coeff = 1;
        int j = 1;
        
        while (currNum > 0) {
            newNum += currNum % 10 * coeff; // Има ли нужда от скоби?
            coeff *= 10;
            currNum /= 100;
        }
        if (newNum != 0 && i % newNum == 0) {
            std::cout << '(' << i << ',' << newNum << ')' << '\n';
        }
    }
    return 0;
}
```

Делим на 100 числото, за да пропуснем цифрите на четни позиции отдясно наляво. Друг начин е да използваме брояч:

```c++
int j = 1;
while (currNum > 0) {
    if (j % 2 == 1) {
        newNum += currNum % 10 * coeff;
        coeff *= 10;
    }
    currNum /= 100;
    ++j;
}
```

## Задача 8

```c++
#include <iostream>

int main() {
    unsigned num;
    std::cin >> num;
    unsigned sum = 0;
    for (unsigned i = 2; i <= num; ++i) {
        bool isPrime = true;
        for (unsigned j = 2; j * j <= i; ++j) {
            if (i % j == 0) {
                isPrime = false;
                break;
            }
        }
        if (num % i == 0 && isPrime) {
            sum += i;
        }
    }
    std::cout << "sum: " << sum;
    return 0;
}
```

Стандартно решение - всяко число от 2 до `num` го събираме, ако е прост делител на `num`. 
- Какво ще кажете за това решение? Прави ли излишен брой проверки и защо? Оправете го.
- Как да променим кода на задача 5, за да решава тази задача?

## Задача 9

```c++
#include <iostream>

int main() {
    unsigned num;
    std::cin >> num;
    while (num != 0 && num % 2 == 0) {
        num /= 2;
    }
    std::cout << (num == 1 ? "power of 2" : "not power of two");
    return 0;
}
```

## Задача 10

```c++
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    if (n <= 0) {
        std::cout << "expected at least one number to enter";
        return 1;
    }
    double number;
    std::cin >> number;
    double sum = number;
    double min = number;
    double max = number;
    for (int i = 0; i < n - 1; ++i) {
        std::cin >> number;
        if (number > max) {
            max = number;
        }
        if (number < min) {
            min = number;
        }
        sum += number;
    }
    std::cout << "min: " << min << '\n';
    std::cout << "max: " << max << '\n';
    std::cout << "avg: " << sum / n << '\n';
    return 0;
}
```

## Задача 11

```c++
#include <iostream>
#include <cmath>

int main() {
    int num;
    std::cin >> num;
    if (num < 0) {
        std::cout << "num is not narcissistic";
        return 1;
    }

    int copyNum = num;
    int countDigits = 0;
    while (num > 0) {
        ++countDigits;
        num /= 10;
    }

    int sum = 0;
    num = copyNum;
    while (num > 0) {
        int currDigit = num % 10;
        sum += std::pow(currDigit, countDigits);
        num /= 10;
    }

    std::cout << (sum == copyNum ? "narcissistic" : "not narcissistic");
    return 0;
}
```

Може ли едно отрицателно число да е нарцистично?

## Задача 12

```c++
#include <iostream>

int main() {
    for (int i = 100; i <= 999; ++i) {
        int sumDigits = 0;
        int currNumber = i;
        while (currNumber > 0) {
            sumDigits += currNumber % 10;
            currNumber /= 10;
        }
        
        currNumber = i;
        int reversedNumber = 0;
        while (currNumber > 0) {
            reversedNumber = reversedNumber * 10 + currNumber % 10;
            currNumber /= 10;
        }

        if (sumDigits >= 10 && sumDigits <= 27 && reversedNumber == i) {
            std::cout << i << '\n';
        }
    }
    return 0;
}
```

## Задача 13

```c++
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (i < j) {
                std::cout << '+';
            }
            else if (i == j) {
                std::cout << 'o';
            }
            else {
                std::cout << '-';
            }
        }
        std::cout << '\n';
    }
    return 0;
}
```

## Задача 14

```c++
#include <iostream>

// 00:00 -> 23:59
// h1h2:m1m2

int main() {
    for (int h1 = 0; h1 <= 2; ++h1) {
        for (int h2 = 0; h2 <= 9; ++h2) {
            if (h1 == 2 && h2 >= 4) {
                break;
            }
            for (int m1 = 0; m1 <= 5; ++m1) {
                for (int m2 = 0; m2 <= 9; ++m2) {
                    std::cout << h1 << h2 << ':' << m1 << m2 << '\n';
                }
            }
        }
    }
    return 0;
}
```


