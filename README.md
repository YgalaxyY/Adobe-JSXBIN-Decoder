# Adobe JSXBIN Decoder


[![.NET](https://img.shields.io/badge/.NET-4.5-blue.svg)](https://dotnet.microsoft.com/download/dotnet-framework/net45)
[![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)](https://www.microsoft.com/windows)
[![GitHub stars](https://img.shields.io/github/stars/ygalaxyy/adobe-jsxbin-decoder.svg?style=social&label=Star)](https://github.com/ygalaxyy/adobe-jsxbin-decoder)

**Adobe JSXBIN Decoder** — это приложение на C# для декодирования бинарного формата JSXBIN в читаемый JSX код. JSXBIN используется Adobe для защиты скриптов автоматизации в Photoshop, Illustrator и других продуктах Creative Suite.

## 🎯 Motivation

### Проблема
Adobe хранит скрипты автоматизации в проприетарном бинарном формате JSXBIN, что создает следующие проблемы:
- **Отсутствие аудита безопасности** — невозможно проверить код на уязвимости
- **Сложность отладки** — ошибки невозможно локализовать без исходного кода
- **Потеря наследия** — старые инструменты становятся недоступными для модификации
- **Закрытая экосистема** — разработчики не могут изучать и улучшать существующие решения

### Решение
Adobe JSXBIN Decoder восстанавливает читаемую структуру кода через:
- **Парсинг AST** — построение полного абстрактного синтаксического дерева
- **Сохранение логики** — точное восстановление алгоритмов и структур данных
- **Форматирование** — генерация читаемого JSX кода с правильной индентацией
- **Отладочную информацию** — детальная визуализация процесса декодирования

### Юридический дисклеймер
> **⚠️ Важно:** Данный инструмент предназначен исключительно для образовательных целей, аудита безопасности и восстановления доступа к собственным наработкам. Автор не несет ответственности за неправомерное использование или нарушение лицензионных соглашений стороннего ПО.

## 🏗️ Архитектура

```mermaid
graph LR
    A[JSXBIN Binary] --> B[Header Parser]
    B --> C[Version Detection]
    C --> D[Binary Stream Scanner]
    D --> E[AST Builder]
    E --> F[Node Decoders]
    F --> G[JSX Generator]
    G --> H[JsBeautifier]
    H --> I[Readable JSX]
    
    style A fill:#4a90e2,color:#ffffff,stroke:#2c5aa0,stroke-width:2px
    style I fill:#5cb85c,color:#ffffff,stroke:#357a35,stroke-width:2px
    style E fill:#f0ad4e,color:#000000,stroke:#d58512,stroke-width:2px
    style B fill:#5bc0de,color:#000000,stroke:#31b0d5,stroke-width:2px
    style C fill:#5bc0de,color:#000000,stroke:#31b0d5,stroke-width:2px
    style D fill:#5bc0de,color:#000000,stroke:#31b0d5,stroke-width:2px
    style F fill:#5bc0de,color:#000000,stroke:#31b0d5,stroke-width:2px
    style G fill:#5bc0de,color:#000000,stroke:#31b0d5,stroke-width:2px
    style H fill:#5bc0de,color:#000000,stroke:#31b0d5,stroke-width:2px
```

### Процесс декодирования
1. **Анализ заголовка** — извлечение версии и метаданных
2. **Сканирование потока** — последовательное чтение маркеров
3. **Построение AST** — создание иерархии узлов синтаксического дерева
4. **Декодирование узлов** — преобразование каждого узла в JSX конструкцию
5. **Генерация кода** — сборка JSX из AST
6. **Форматирование** — применение JsBeautifier для читаемости

## 🚀 Быстрый старт

### Установка и сборка

#### Требования

- **Windows** 7 или выше
- **.NET Framework 4.5** или выше
- **Visual Studio 2015+** (для сборки из исходников)

#### Сборка из исходников

```bash
# Клонирование репозитория
git clone https://github.com/yourusername/jsxbin-to-jsx-converter.git
cd jsxbin-to-jsx-converter

# Сборка проекта
msbuild jsxbin_to_jsx.sln /p:Configuration=Release

# Или через Visual Studio:
# 1. Откройте jsxbin_to_jsx.sln
# 2. Выберите Configuration: Release
# 3. Build -> Build Solution
```

#### Готовые сборки

Скачайте последнюю версию из [Releases](https://github.com/yourusername/jsxbin-to-jsx-converter/releases)

## 📖 Использование

### Базовый синтаксис

```bash
jsxbin_to_jsx [-v] <input.jsxbin> <output.jsx>
```

### Примеры использования

#### Простое декодирование

```bash
jsxbin_to_jsx script.jsxbin decoded_script.jsx
```

#### Декодирование с отладочной информацией

```bash
jsxbin_to_jsx -v script.jsxbin decoded_script.jsx > debug_output.txt
```

#### Пакетная обработка (Windows batch)

```batch
@echo off
for %%f in (*.jsxbin) do (
    echo Декодирование %%f...
    jsxbin_to_jsx "%%f" "%%~nf.jsx"
)
echo Готово!
```

### Флаги и параметры

| Флаг | Описание                                                                   |
| -------- | ---------------------------------------------------------------------------------- |
| `-v`   | Выводить дерево разбора (AST) в stdout для отладки |

## 🔧 Как это работает?

### Архитектура проекта

```
jsxbin_to_jsx/
├── Program.cs                 # Точка входа и CLI интерфейс
├── JsxbinDecoding/           # Ядро декодера
│   ├── AbstractNode.cs       # Базовый класс для всех узлов AST
│   ├── NodeType.cs           # Перечисление типов узлов
│   ├── ScanState.cs          # Состояние сканера бинарного потока
│   └── [50+ файлов]          # Декодеры для различных конструкций JSX
├── jsxbin_to_jsx.Tests/      # Юнит-тесты
└── libs/                     # Внешние зависимости
```

### Процесс декодирования

1. **Анализ заголовка** — извлечение версии JSXBIN формата
2. **Парсинг бинарного потока** — последовательное чтение маркеров
3. **Построение AST** — создание абстрактного синтаксического дерева
4. **Генерация JSX** — преобразование AST в читаемый код
5. **Форматирование** — beautify с помощью JsBeautifier

## 📊 Совместимость

| Feature | Support | Notes |
|---------|---------|-------|
| **ES5 Syntax** | ✅ Full | Core JavaScript features supported |
| **XML (E4X)** | ⚠️ Partial | Namespaces support included |
| **JSXBIN v1.0** | ✅ Yes | Tested on Photoshop CS6+ |
| **JSXBIN v2.0** | ✅ Yes | Tested on Photoshop 2024+ |
| **JSXBIN v2.1** | 🚧 Beta | In development, experimental |
| **Windows 7+** | ✅ Yes | Native support |
| **Linux/macOS** | ❌ No | .NET Framework limitation |

### Поддерживаемые конструкции

#### 🔄 Control Flow (Поток управления)
- Условные операторы: `if`, `else if`, `else`
- Циклы: `for`, `while`, `do-while`, `for-in`
- Исключения: `try-catch-finally`, `throw`
- Переключатели: `switch-case`
- Переходы: `break`, `continue`, `return`

#### 📦 Data Types (Типы данных)
- Примитивы: `string`, `number`, `boolean`, `null`, `undefined`
- Коллекции: `Array`, `Object` literals
- Функции: declarations, expressions, arrows
- XML: E4X literals, namespaces, accessors
- RegExp: регулярные выражения

#### 🔍 Scoping (Область видимости)
- Переменные: `var`, `let`, `const`
- Функции: hoisting, closures
- Пространства имен: XML namespaces
- Контекст: `this`, `with` statement

## 🧪 Тестирование

### Запуск тестов

```bash
# Через Visual Studio
Test -> Run All Tests

# Через командную строку
vstest.console.exe jsxbin_to_jsx.Tests\bin\Release\jsxbin_to_jsx.Tests.dll
```

### Структура тестов

- **Юнит-тесты** для каждого типа узла AST
- **Интеграционные тесты** для полных файлов
- **Регрессионные тесты** для совместимости версий

## 📁 Структура проекта

```
jsxbin-to-jsx-converter/
├── jsxbin_to_jsx/            # Основное приложение
│   ├── Program.cs           # CLI интерфейс
│   ├── JsxbinDecoding/      # Ядро декодера
│   ├── App.config           # Конфигурация приложения
│   └── Properties/           # Настройки сборки
├── jsxbin_to_jsx.Tests/     # Тесты
├── libs/                    # Внешние библиотеки
├── LICENSE                  # Лицензия MIT
├── README.md               # Этот файл
└── jsxbin_to_jsx.sln       # Solution файл
```

## 🔍 Отладка

### Использование флага `-v`

Флаг `-v` выводит детальное дерево разбора:

```bash
jsxbin_to_jsx -v example.jsxbin output.jsx
```

Пример вывода:

```
StatementList
    ExprNode
        AssignmentExpr
            IdNode: test
            ValueNode: 5
    IfStatement
        BinaryExpr
            IdRefExpr: test
            ValueNode: 5
        StatementList
            ExprNode
                FunctionCallExpr
                    IdNode: doSomething
```

### Поиск проблем

Если декодирование не удалось:

1. Проверьте версию JSXBIN формата
2. Используйте флаг `-v` для анализа проблемного места
3. Создайте issue на GitHub с примером файла

## 🤝 Внесение вклада

Мы приветствуем вклад в проект! Пожалуйста, ознакомьтесь с [CONTRIBUTING.md](CONTRIBUTING.md).

### Как начать

1. Fork репозитория
2. Создайте feature branch (`git checkout -b feature/amazing-feature`)
3. Внесите изменения
4. Добавьте тесты
5. Отправьте pull request

## 📋 Roadmap

- [ ] Поддержка .NET Core/.NET 5+ для кроссплатформенности
- [ ] GUI интерфейс для удобного использования
- [ ] Плагин для VS Code
- [ ] Обратное преобразование (JSX → JSXBIN)
- [ ] Поддержка более новых версий JSXBIN

## 🐛 Проблемы и ограничения

### Известные ограничения

- **Только Windows** — зависимость от .NET Framework
- **Только декодирование** — обратное преобразование не поддерживается
- **Версионная зависимость** — некоторые новые конструкции могут не поддерживаться

### Частые проблемы

#### "Decoding failed"

- Проверьте целостность JSXBIN файла
- Убедитесь, что файл не поврежден
- Попробуйте использовать флаг `-v` для диагностики

#### "Unsupported node type"

- Создайте issue с примером файла
- Временно можно использовать UnknownNode2 как заглушку

## 📞 Контакты

- **GitHub Issues**: [Сообщить о проблеме](https://github.com/yourusername/jsxbin-to-jsx-converter/issues)
- **GitHub Discussions**: [Обсуждения](https://github.com/yourusername/jsxbin-to-jsx-converter/discussions)

---

**⭐ Если проект полезен — поставьте звезду!**
