# cpp1901
##### Lessons and projects
----
### Lessons:
----
| Lesson №      | Name                                                   | Path          | TIMESTAMP  |
|---------------|:-------------------------------------------------------|:-------------:|:----------:|
| Lesson 1      | Introductin to C++, Hello, world                       | cpp/lesson1/  | 00.00.0000 |
| Lesson 2      | Arrays, tasks                                          | cpp/lesson2/  | 00.00.0000 |
| Lesson 3      | Types                                                  | cpp/lesson3/  | 00.00.0000 |
| Lesson 4      | Math in C++                                            | cpp/lesson4/  | 00.00.0000 |
| Lesson 5      | Math functions                                         | cpp/lesson5/  | 00.00.0000 |
| Lesson 6      | Functions                                              | cpp/lesson6/  | 00.00.0000 |
| Lesson 7      | Tasks, money converter                                 | cpp/lesson7/  | 00.00.0000 |
| Lesson 8      | Description not proveded                               | -             | 00.00.0000 |
| Lesson 9      | Strictures in C++, compiling program as multiple files | cpp/lesson9/  | 00.00.0000 |
| Lesson 10     | Boolalpha                                              | cpp/lesson10/ | 00.00.0000 |
| Lesson 11     | Translate integers, binary, decimal, hexdecimal        | cpp/lesson11/ | 00.00.0000 |
| Lesson 12     | Repeat arrays                                          | cpp/lesson12/ | 00.00.0000 |
| Lesson 13     | 2D arrays                                              | cpp/lesson13/ | 00.00.0000 |
| Lesson 14     | Description not proveded                               | -             | 00.00.0000 |
| Lesson 15     | Exams                                                  | cpp/lesson15/ | 00.00.0000 |
| Lesson 16     | Github                                                 | cpp/lesson16/ | 00.00.0000 |
----
### Example: Binary Decoder (RU)
###### Path: cpp/lesson11/bin.cpp
----
```cpp
/*=====================================================
 * Перевод двоичного кода в десятичный методом сложения
 * Создал: xXDima212DimaXx
 *
 * Лицензия: Свободный доступ и модификация
 *
 * Как это работает?
 *
 * Создается массив данных (пользовательские данные),
 * в который пользователь заносит двоичное значение.
 * Затем создается переменная кратная 2 (ее значение
 * зависит от длины введенных данных. Например для
 * 1 байта это 128). Затем если первая цифра данных
 * равна 1, к конечному значению прибавляется
 * значение этой переменноя, и наоборот если первая
 * цифра равна 0, то прибавления не происходит.
 * Затем та переменная (кратная 2) делится на 2 и
 * действие повторяется, только уже проверяется вторая
 * цифра в двоичном значении. Цикл выполняется пока
 * переменная, которая кратна 2 не достигает значения 1
 * и пока в двоичных данных не закончились цыфры для
 * проверки (их количество равно размеру массива с
 * пользовательскими данными). После этого полученное
 * значение выводиться на экран.
 *===================================================*/

#include <iostream>
#include <cstdlib>
#include <limits>
#include <cstring>

int convert(char val[]);

int main (void) {
    // Значение, которое вводит пользователь (1 байт)
    char value[8] = {};

    // Для проверки длины (Debug)
    // char vb[] = "";

    // Запрос пользовательского ввода
    std::cout << "Enter 1 byte: ";
    std::cin >> value;

    // Debug
    // if (vb.length() == 8) {
    //     value = vb;
    // } else {
    //     std::cout << "Incorect length of data. You can use only 8 digits!" << std::endl;
    //     return 1;
    // }

    // Исправление бага при вводе неверного типа данных
    if ((std::cin.fail() == 0)) {
        // Если пользователь ввел правильный тип данных, продолжаем выполнение
    } else {
        // Если тип данных некорректный, то завершаем программу, выдав ошибку
        std::cin.clear();
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Incorect type of data. Value \"" << value << "\" not allowed. You can use only 0 or 1!" << std::endl;
        return 1;
    }

    for (int g = 0; g < sizeof(value); g++) {
        if ((value[g] == '0') || (value[g] == '1')) {

        } else {
            std::cout << "Incorect type of data. Value \"" << value << "\" not allowed. You can use only 0 or 1!" << std::endl;
            return 1;
        }
    }

    // Debug
    // std::cout << value << std::endl;

    // Вызов условной функции, которая проверяет значение введенные данные и выводит результат на экран
    std::cout << "Decoded value: " << convert(value) << std::endl;

    return 0;
}

// Условная функция, которая проверяет значение переменной val
int convert(char val[]) {
    // Debug
    // std::cout << val << std::endl;

    // R - конечное значение, которое выведет программа
    int r = 0;

    // J для откладки. По желанию можно удалить и использовать val[int] в проверочном условии
    int j = 0;

    // plus - переменная, помогающая вычислить значение r (см. код ниже)
    int plus = 256;

    // Цикл проверки. Выполняется n-ое кол-во раз, где n - число Бит (1 Байт = 8 Бит)
    for (int i = 0; i < sizeof(val); i++) {
        /*=====================================================
         * Раскоментировать если программа работает неправильно
         * (Режим откладки)
         * std::cout << "[" << i << "]" << "\t";
         * std::cout << val[i] << "\t";
         *===================================================*/

        // J для откладки. По желанию можно заменить на val[int] в проверочном условии
        j = val[i];

        /*=====================================================
         * Раскоментировать если программа работает неправильно
         * (Режим откладки)
         * std::cout << "Debug j: " << j << "\t";
         * std::cout << "Debug j - 48: " << (j - 48) << "\t";
         *===================================================*/

        // Необходимо для расшифровки двоичного кода методом сложения
        plus = plus/2;

        // Проверка
        if ((j - 48) == 1) {
            r = r + plus;

            // Debug
            // std::cout << "\t 1\t" << r << " Debug plus: " << plus << std::endl;
        } else {
            // Debug
            // std::cout << "\t 0\t" << r << " Debug plus: " << plus << std::endl;
        }

    }

    // Возврат результата выполнения программы
    return r;
}
```
----
### Example: Celsius to Fahrenheit (Exam task)
###### Path: cpp/lesson15/cf.cpp
----
```cpp
#include <iostream>
#include <cstdlib>
#include <limits>

using namespace std;

int main (void)
{
    cout << "Celsius to Fahrenheit" << endl;
    int N = 0;
    int M = 0;
    cout << "From: ";
    cin >> N;
    cout << "To: ";
    cin >> M;

    for (;N < M; N++) {
        cout << N << "°C\t" << (N*1.8)+32 << "°F" << endl;
    }
    return 0;
}
```
----
### Projects:
----
| Name                                 | Version | Path                        | TIMESTAMP  |
|--------------------------------------|:-------:|:---------------------------:|:----------:|
| Tic Tac Toe (The final project)      | 1.1     | [cpp/projects/tictactoe/1.1](https://github.com/xXDima212DimaXx/cpp1901/tree/master/projects/tictactoe/1.1)  | 00.00.0000 |
| Tic Tac Toe (The final project)      | 1.2     | [cpp/projects/tictactoe/1.2](https://github.com/xXDima212DimaXx/cpp1901/tree/master/projects/tictactoe/1.2)  | 00.00.0000 |
| Description not provided             | 0.0     | [cpp/projects/newproject](https://github.com/xXDima212DimaXx/cpp1901/tree/master/projects/newproject)     | 00.00.0000 |
----
### Useful links:
----
> 1. First item
> 2. Second item
> 3. Third item
> 4. Fourth item

![Linux](https://d33wubrfki0l68.cloudfront.net/e7ed9fe4bafe46e275c807d63591f85f9ab246ba/e2d28/assets/images/tux.png)

Site [jarvis](https://jarvis.studio).
hjthjth