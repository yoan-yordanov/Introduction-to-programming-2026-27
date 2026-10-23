# Седмица 3 - Цикли - решения

## Задача 1

Започваме с `result = 1` и умножаваме резултата по `n` точно `k` пъти. Така получаваме \(n^k\). Използваме `long long`, за да можем да съхраняваме по-големи цели числа.

```cpp
#include <iostream>

int main()
{
    int n, k;
    std::cin >> n >> k;

    long long result = 1;
    for (int i = 0; i < k; i++)
    {
        result *= n;
    }

    std::cout << result << '\n';
}
```

## Задача 2

Факториелът на `n` е произведението на всички цели числа от `1` до `n`. Започваме с `result = 1` и обхождаме числата от `n` надолу до `1`, като умножаваме всяко от тях към резултата.

```cpp
#include <iostream>

int main()
{
    int n;
    std::cin >> n;

    long long result = 1;
    for (int i = n; i > 0; i--)
    {
        result *= i;
    }

    std::cout << result;
}
```

## Задача 3

Проверяваме дали числото има делител между `2` и квадратния корен от него. Ако намерим такъв делител, числото не е просто и можем да прекратим цикъла с `break`. Числата, които са по-малки от `2`, не са прости. Условието `i * i <= num` включва и случая, в който числото е точен квадрат.

```cpp
#include <iostream>

int main()
{
    int num;
    std::cin >> num;

    if (num <= 1)
    {
        std::cout << "Not prime";
        return 1;
    }

    bool isPrime = true;
    for (int i = 2; i * i <= num; i++)
    {
        if (num % i == 0)
        {
            isPrime = false;
            break;
        }
    }

    std::cout << (isPrime ? "Prime" : "Not prime");
}
```

## Задача 4

Използваме `a % 10`, за да вземем последната цифра на `a`, а след това `a /= 10`, за да я премахнем. Така намираме сумата на цифрите на `a`. По същия начин намираме произведението на цифрите на `b`. За сумата започваме от 0, а за произведението - от 1. Накрая сравняваме двете стойности и извеждаме резултата като `true` или `false`.

```cpp
#include <iostream>

int main()
{
    int a, b;
    std::cin >> a >> b;

    int sumA = 0;
    int productB = 1;

    while (a > 0)
    {
        sumA += a % 10;
        a /= 10;
    }

    while (b > 0)
    {
        productB *= b % 10;
        b /= 10;
    }

    std::cout << std::boolalpha << (sumA == productB);
}
```

## Задача 5

Използваме цикъл `do-while`, защото трябва да прочетем поне едно число. Всяко въведено число се прибавя към `sum`, включително нулата, която служи за край на въвеждането. След прочитането на `0` условието става невярно и цикълът приключва.

```cpp
#include <iostream>

int main()
{
    int num;
    int sum = 0;

    do {
        std::cin >> num;
        sum += num;
    } while (num != 0);

    std::cout << sum;
}
```

## Задача 6

Сравняваме последната цифра с цифрата непосредствено преди нея. Ако последната цифра е по-голяма, цифрите не са в намаляващ ред и задаваме `isDecreasing = false`. След всяка проверка премахваме последната цифра. В този код равните съседни цифри са позволени.

```cpp
#include <iostream>

int main()
{
    int num;
    std::cin >> num;

    if (num < 0)
    {
        std::cout << "Only positive numbers!\n";
        return 1;
    }

    bool isDecreasing = true;
    while (num > 10)
    {
        int lastDigit = num % 10;
        int secToLastDigit = (num / 10) % 10;

        if (lastDigit > secToLastDigit)
        {
            isDecreasing = false;
            break;
        }

        num /= 10;
    }

    std::cout << std::boolalpha << isDecreasing;
}
```

## Задача 7

Обхождаме цифрите на числото отдясно наляво. Когато намерим нова най-голяма цифра, предишната най-голяма става втората най-голяма. В противен случай, ако цифрата е по-голяма от текущата втора най-голяма, обновяваме само нея.

```cpp
#include <iostream>

int main()
{
    int num;
    std::cin >> num;

    int biggestDigit = -1;
    int secToBiggestDigit = -1;

    while (num > 0)
    {
        int lastDigit = num % 10;

        if (lastDigit > biggestDigit)
        {
            secToBiggestDigit = biggestDigit;
            biggestDigit = lastDigit;
        }
        else if (lastDigit < biggestDigit && lastDigit > secToBiggestDigit)
        {
            secToBiggestDigit = lastDigit;
        }

        num /= 10;
    }

    std::cout << secToBiggestDigit;
}
```

## Задача 8

Запазваме първоначалното число в `num`, защото ще променяме `numCopy`, за да обърнем цифрите му. При всяка итерация местим цифрите на `reversedNum` с една позиция наляво и добавяме последната цифра на `numCopy`. Ако обърнатото число е равно на оригиналното, числото е палиндром.

```cpp
#include <iostream>

int main()
{
    int num;
    std::cin >> num;
    int numCopy = num;

    int reversedNum = 0;
    while (numCopy > 0)
    {
        reversedNum *= 10;
        reversedNum += numCopy % 10;
        numCopy /= 10;
    }

    std::cout << std::boolalpha << (num == reversedNum);
}
```

## Задача 9

За да преобразуваме числото в двоична бройна система, намираме остатъка при деление на `2` и го използваме като поредна двоична цифра. След това делим числото на `2` и повтаряме, докато стане `0`. Тъй като остатъците се получават от най-малката към най-голямата позиция, използваме степените на `10`, за да ги подредим в правилния ред. Така първият остатък ще е най-дясната цифра в резултата, а последният остатък ще е най-лявата.

```cpp
#include <iostream>
#include <cmath>

int main()
{
    int num;
    std::cin >> num;

    long long binaryRes = 0;
    for (int i = 0; num != 0; i++)
    {
        int remainder = num % 2;
        binaryRes += remainder * static_cast<long long>(std::pow(10, i));
        num /= 2;
    }

    std::cout << binaryRes;
}
```