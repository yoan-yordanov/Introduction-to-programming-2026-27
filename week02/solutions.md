# Решения на задачите от седмица 2

[Задача 1](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-1)<br>
[Задача 2](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-2)<br>
[Задача 3](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-3)<br>
[Задача 4](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-4)<br>
[Задача 5](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-5)<br>
[Задача 6](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-6)<br>
[Задача 7](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-7)<br>
[Задача 8](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-8)<br>
[Задача 9](https://github.com/yoan-yordanov/Introduction-to-programming-2026-27/blob/test/week02/solutions.md#задача-9)<br>

## Задача 1

```c++
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    if (n % 3 == 0 && n % 5 == 0) {
        std::cout << "FizzBuzz";
    }
    else if (n % 5 == 0) {
        std::cout << "Buzz";
    }
    else if (n % 3 == 0) {
        std::cout << "Fizz";
    }
    else {
        std::cout << n;
    }
    return 0;
}
```
При този синтаксис на оператора if else при удовлетворяване на някое условие следващите условия се пропускат. Затова редът на условията е от значение. Нека `n = 15`. Ако `n % 3 == 0` е преди `n % 3 == 0 && n % 5 == 0`, то ще изведе Fizz вместо FizzBuzz.

## Задача 2

```c++
#include <iostream>

int main() {
    double a, b, c;
    std::cin >> a >> b >> c;

    if (a <= 0 || b <= 0 || c <= 0) {
        std::cout << "Sides of a triangle must be positive real numbers";
        return 1; // програмата приключва изпълнението си, 1 индикира, че тя е завършила неуспешно
    }

    bool isValidTriangle = a + b > c && a + c > b && b + c > a;
    // булевият израз се пресмята отляво надясно. Ред на операторите: +, >, &&, =
    if (isValidTriangle) {
        std::cout << "valid";
    }
    else {
        std::cout << "invalid";
    }
    //std::cout << "\n" << (isValidTriangle ? "valid" : "invalid");
    return 0;   
}
```
Триъгълник е валиден, ако сборът на всеки две страни е по-голям от третата. Показан е тернарният оператор като коментар. Скобите са необходими, тъй като операторът `<<` е с по-висок приоритет от тернарния `?:`.

## Задача 3

```c++
#include <iostream>

int main() {
    int x, y;
    std::cin >> x >> y;
    if (x == 0 && y == 0) {
        std::cout << "point lies at origin";
    }
    else if (x == 0 && y > 0) {
        std::cout << "point lies on positive y-axis";
    }
    else if (x == 0 && y < 0) {
        std::cout << "point lies on negative y-axis";
    }
    else if (x > 0 && y == 0) {
        std::cout << "point lies on positive x-axis";
    }
    else if (x < 0 && y == 0) {
        std::cout << "point lies on negative x-axis";
    }
    else if (x > 0 && y > 0) {
        std::cout << "first quadrant";
    } 
    else if (x < 0 && y > 0) {
        std::cout << "second quadrant";
    }
    else if (x < 0 && y < 0) {
        std::cout << "third quadrant";
    }
    else {
        std::cout << "fourth quadrant";
    }
    return 0;
}
```
Редът на условията не е от значение, защото са взаимноизключващи се. Защо са точно 9 на брой?

## Задача 4

```c++
#include <iostream>
#include <cmath>

int main()
{
    double a, b, c;
    std::cin >> a >> b >> c;

    if (a == 0) {
        std::cout << "a cannot be zero";
        return 1; // програмата приключва, не се изпълнява нищо след това
    }

    double d = b * b - 4 * a * c;

    double x1 = (-b - std::sqrt(d)) / (2 * a);
    double x2 = (-b + std::sqrt(d)) / (2 * a);

    bool doesEqHaveRealRoots = d >= 0;
    bool doesEqHaveDoubleRoot = fabs(d) <= 1e-14;
    bool doesEqHaveIntegerRoot = (int)x1 == x1 || (int)x2 == x2;
    bool isSumDiffFromProduct = fabs(x1 + x2 - x1 * x2) <= 1e-14;
}
```
Реалните числа не могат да се представят точно в паметта. Затова, за да се провери дали две реални числа са равни, трябва абсолютната стойност на разликата им да е по-малка от някакво малко положително число.

## Задача 5

```c++
#include <iostream>
#include <windows.h>

int main() {
    SetConsoleOutputCP(CP_UTF8);
    int grade;
    std::cin >> grade;
    
    switch (grade) {
        case 2:
            std::cout << "слаб";
            break;
        case 3:
            std::cout << "среден";
            break;
        case 4:
            std::cout << "добър";
            break;
        case 5:
            std::cout << "много добър";
            break;
        case 6:
            std::cout << "отличен";
            break;
        default:
            std::cout << "невалидна оценка";
            break;
    }
    
    if (grade == 2) {
        std::cout << "слаб";
    }
    else if (grade == 3) {
        std::cout << "среден";
    }
    else if (grade == 4) {
        std::cout << "добър";
    }
    else if (grade == 5) {
        std::cout << "много добър";
    }
    else if (grade == 6) {
        std::cout << "отличен";
    }
    else {
        std::cout << "невалидна оценка";
    }
    return 0;
}
```

## Задача 6

```c++
#include <iostream>

int main() {
    int month;
    std::cin >> month;

    switch (month)
    {
        case 12: case 1: case 2: 
            std::cout << "winter";
            break;
        case 3: case 4: case 5:
            std::cout << "spring";
            break;
        case 6: case 7: case 8:
            std::cout << "summer";
            break;
        case 9: case 10: case 11:
            std::cout << "autumn";
            break;
        default:
            std::cout << "invalid month";
            break;
    }
    return 0;
}
```

## Задача 7

```c++
#include <iostream>
#include <windows.h>

int main() {
    int temperature;
    bool isRaining;
    bool isBlowingWind;

    SetConsoleOutputCP(CP_UTF8);
    std::cout << "Enter temperature: ";
    std::cin >> temperature;
    std::cout << "Is it raining? (0/1): ";
    std::cin >> isRaining;
    std::cout << "Is wind blowing? (0/1): ";
    std::cin >> isBlowingWind;

    if (temperature < 0) {
        std::cout << "Облечи дебело яке и шапка.";
        if (isRaining) {
            std::cout << " Добави и чадър.";
        }
    }
    else if (temperature >= 0 && temperature <= 15) {
        std::cout << "Облечи леко яке.";
        if (isBlowingWind) {
            std::cout << " Вземи си и ветроустойчиво горнище.";
        }
    }
    else {
        std::cout << "Облечи тениска.";
        if (isRaining) {
            std::cout << " Носи си и чадър.";
        }
    }
    return 0;
}
```

## Задача 8

```c++
#include <iostream>

int main() {
    int day, year, month;
    std::cout << "Enter day, month, year: ";
    std::cin >> day >> month >> year;

    bool isLeapYear = (year % 4 == 0 && (!(year % 100 == 0) || year % 400 == 0));

    bool isValidYear = year >= 1000 && year <= 2100;
    bool isValidMonth = month >= 1 && month <= 12;

    if (!isValidYear) {
        std::cout << "not valid date. Year must be in [1000,2100]\n";
        return 1; // не се изпълнява нищо след това
    }
    if (!isValidMonth) {
        std::cout << "not valid date. Month must be in [1,12]\n";
        return 2; // не се изпълнява нищо след това
    }

    bool isValidDay;
    switch (month) {
        case 1: case 3: case 5: case 7: case 8: case 10: case 12:
            isValidDay = day >= 1 && day <= 31;
            break;
        case 4: case 6: case 9: case 11:
            isValidDay = day >= 1 && day <= 30;
            break;
        case 2:
            isValidDay = day >= 1 && day <= (isLeapYear ? 29 : 28);
            break;
        // няма нужда от default; <some error>; break;
        // понеже преди switch месецът се проверява дали е валиден
    }

    if (isValidDay) // ако годината и месеца са невалидни, то програмата няма да стигне дотук
    {
        std::cout << day << '.' << month << '.' << year << " is valid date\n";
    }
    else {
        std::cout << day << '.' << month << '.' << year << " is not valid date\n";
        return 3;
    }

    // which is next date?

    int nextDay = day + 1; // при повечето дати ще е това
    // само при край на месеца и на последния ден от годината трябва изрично да се сменят в switch
    int nextMonth = month; 
    int nextYear = year;
    int daysInFebr;

    // тъй като датата е валидна, то няма нужда от всички проверки за ден и месец
    switch (month) {
        case 1: case 3: case 5: case 7: case 8: case 10:
            if (day == 31) {
                nextDay = 1;
                nextMonth = month + 1;
            }
            break;
        case 4: case 6: case 9: case 11:
            if (day == 30) {
                nextDay = 1;
                nextMonth = month + 1;
            } 
            break;
        case 2:
            daysInFebr = isLeapYear ? 29 : 28;
            if (day == daysInFebr) {
                nextDay = 1;
                nextMonth = month + 1;
            }
            break;
        case 12:
            if (day == 31) {
                nextDay = 1;
                nextMonth = 1;
                nextYear = year + 1;
            }
            break;
    }

    std::cout << "next valid date: " << nextDay << '.' << nextMonth << '.' << nextYear << '\n';
    return 0;
}
```

## Задача 9

```c++
#include <iostream>

int main() {
    int startX, startY, goalX, goalY;
    std::cin >> startX >> startY >> goalX >> goalY;

    // проверка за валидност на координатите на двете полета
    if (startX < 0 || startY > 7 || goalX < 0 || goalY > 7) {
        std::cout << "invalid coordinates";
        return 1;
    }

    // цар
    if (startX == goalX && startY + 1 == goalY 
        || startX + 1 == goalX && startY + 1 == goalY
        || startX + 1 == goalX && startY == goalY
        || startX + 1 == goalX && startY - 1 == goalY
        || startX == goalX && startY - 1 == goalY
        || startX - 1 == goalX && startY - 1 == goalY
        || startX - 1 == goalX && startY == goalY
        || startX - 1 == goalX && startY + 1 == goalY) 
    {
        std::cout << "king\n";
    }

    // топ
    if (startX == goalX || startY == goalY) {
        std::cout << "rook\n";
    }

    // кон
    if (startX  - 1 == goalX && startY + 2== goalY
        || startX + 1 == goalX && startY + 2 == goalY
        || startX == goalX && startY == goalY
        || startX + 2 == goalX && startY + 1 == goalY
        || startX + 2 == goalX && startY - 1 == goalY
        || startX + 1 == goalX && startY - 2 == goalY
        || startX - 1 == goalX && startY - 2 == goalY
        || startX - 2 == goalX && startY - 1 == goalY
        || startX - 2 == goalX && startY + 1 == goalY) 
    {
        std::cout << "knight\n";
    }
    return 0;
}
```
Не е нужно да се проверява дали потенциален ход на фигура е в рамките на шахматната дъска.
Достатъчно е начално и целево поле да са валидни полета и ходът да е възможен.


