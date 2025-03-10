# SpreadSheet

## Описание
Этот проект представляет собой базовый модуль логики для табличного процессора, подобного Microsoft Excel или Google Sheets. Таблица позволяет вводить текст и формулы в ячейки. Формулы могут включать ссылки на другие ячейки и обрабатываются с использованием ANTLR - мощного генератора парсеров.

Основные возможности:
- Ввод и редактирование данных в ячейках
- Использование формул с арифметическими операциями и ссылками на ячейки
- Обработка ошибок и циклических ссылок

## Основные компоненты

### FormulaParser
- Генерация парсера из грамматики `Formula.g4`
- Поддержка арифметических операций (+, -, *, /)
- Поддержка ссылок на ячейки (например, A1, B2)
- Поддержка числовых литералов (целые и с плавающей точкой)
- Обработка ошибок синтаксиса формул

### Sheet
- Управление ячейками таблицы
- Обработка формул и вычисление значений
- Поддержка пустых ячеек и ячеек за пределами таблицы
- Обработка циклических ссылок между ячейками

### Тесты
Проект включает набор тестов, реализованных в `main.cpp`:
1. **Тесты позиций ячеек**:
   - Преобразование между строковым представлением и координатами
   - Обработка невалидных позиций

2. **Тесты формул**:
   - Арифметические операции
   - Обработка ссылок на ячейки
   - Обработка ошибок (деление на ноль, переполнение)

3. **Тесты обработки ошибок**:
   - Невалидные формулы
   - Циклические ссылки
   - Обработка ошибок значений

## Сборка проекта

### Требования
- CMake (версия 3.8 или выше)
- Компилятор C++ (GCC или MSVC)
- ANTLR 4.13.2 (уже включен в проект)
- JDK (для работы ANTLR)

### Сборка в VS Code
Проект предварительно настроен для сборки в VS Code. Для сборки:

1. Убедитесь, что установлены:
   - Расширение CMake Tools для VS Code
   - Компилятор C++
   - JDK (для работы ANTLR)

2. Откройте папку проекта в VS Code

3. Выберите конфигурацию сборки (Debug/Release)

4. Запустите сборку через меню CMake Tools

### Ручная сборка
1. Создайте директорию для сборки:
   ```bash
   mkdir build
   cd build
   ```

2. Запустите CMake:
   ```bash
   cmake ..
   ```

3. Соберите проект:
   ```bash
   cmake --build .
   ```

## Запуск
После успешной сборки запустите программу:
```bash
./spreadsheet
```

## Пример использования

```cpp
auto sheet = CreateSheet();

// Установка значений в ячейки
sheet->SetCell("A1"_pos, "5");
sheet->SetCell("A2"_pos, "10"); 
sheet->SetCell("B1"_pos, "15");
sheet->SetCell("B2"_pos, "20");

// Создание формул
sheet->SetCell("A3"_pos, "=A1 + A2");  // Сумма столбца A
sheet->SetCell("B3"_pos, "=B1 + B2");  // Сумма столбца B
sheet->SetCell("C1"_pos, "=A1 + B1");  // Сумма строки 1
sheet->SetCell("C2"_pos, "=A2 + B2");  // Сумма строки 2
sheet->SetCell("C3"_pos, "=A3 + B3");  // Общая сумма

// Вывод результатов
std::cout << "\nSpreadsheet Values:\n";
sheet->PrintValues(std::cout);

std::cout << "\nSpreadsheet Formulas:\n"; 
sheet->PrintTexts(std::cout);
```

Результат выполнения:
```
Spreadsheet Values:
5    15    20
10   20    30
15   35    50

Spreadsheet Formulas:
 5      15    =A1+B1
 10     20    =A2+B2
=A1+A2 =B1+B2 =A3+B3
```

## Инструменты разработки
- Язык программирования: C++17
- Сборка: CMake 3.8+
- Компилятор: GCC (MinGW-W64) или MSVC
- Используемые библиотеки: ANTLR 4.13.2
- JDK (для работы ANTLR)
- IDE: Visual Studio Code с поддержкой CMake
