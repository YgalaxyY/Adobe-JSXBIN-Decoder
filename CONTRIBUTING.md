# Contributing to JSXBIN to JSX Converter

Спасибо за интерес к проекту! Мы ценим любую помощь в развитии JSXBIN to JSX Converter.

## 🚀 Как начать

### Требования

- Windows 7 или выше
- .NET Framework 4.5+
- Visual Studio 2015+ или Visual Studio Code
- Базовое понимание C# и JavaScript/JSX

### Настройка окружения

1. **Fork репозитория**

   ```bash
   git clone https://github.com/yourusername/jsxbin-to-jsx-converter.git
   cd jsxbin-to-jsx-converter
   ```
2. **Настройка remotes**

   ```bash
   git remote add upstream https://github.com/original-owner/jsxbin-to-jsx-converter.git
   ```
3. **Сборка проекта**

   ```bash
   msbuild jsxbin_to_jsx.sln /p:Configuration=Debug
   ```

## 📝 Руководство по вкладу

### Типы вкладов

#### 🐛 Исправление багов

1. Проверьте [существующие issues](https://github.com/yourusername/jsxbin-to-jsx-converter/issues)
2. Создайте новый issue с описанием проблемы
3. Fork и создайте branch для исправления
4. Добавьте тесты для воспроизведения и проверки исправления

#### ✨ Новые функции

1. Обсудите идею в [Discussions](https://github.com/yourusername/jsxbin-to-jsx-converter/discussions)
2. Создайте issue с описанием функционала
3. Реализуйте функцию с тестами
4. Обновите документацию

#### 📚 Документация

- Исправления опечаток
- Улучшение примеров
- Переводы на другие языки
- Добавление секций в README

### Процесс разработки

1. **Создайте branch**

   ```bash
   git checkout -b feature/your-feature-name
   # или
   git checkout -b fix/your-bug-fix
   ```
2. **Внесите изменения**

   - Следуйте существующему стилю кода
   - Добавьте комментарии для сложных участков
   - Обновите тесты
3. **Тестирование**

   ```bash
   # Запуск всех тестов
   vstest.console.exe jsxbin_to_jsx.Tests\bin\Debug\jsxbin_to_jsx.Tests.dll

   # Сборка проекта
   msbuild jsxbin_to_jsx.sln /p:Configuration=Release
   ```
4. **Коммит**

   ```bash
   git add .
   git commit -m "feat: add new decoder for XYZ construct"
   ```
5. **Push и Pull Request**

   ```bash
   git push origin feature/your-feature-name
   ```

## 🏗️ Архитектура проекта

### Основные компоненты

#### JsxbinDecoding/

- **AbstractNode.cs** — базовый класс для всех узлов
- **NodeType.cs** — перечисление типов узлов
- **ScanState.cs** — состояние парсера
- **[NodeName].cs** — конкретные реализации узлов

#### Добавление нового узла

1. **Создайте класс узла**

   ```csharp
   public class NewNode : AbstractNode
   {
       public override string Marker => "M";
       public override NodeType NodeType => NodeType.NewNode;

       public override void Decode()
       {
           // Логика декодирования
       }

       public override string PrettyPrint()
       {
           // Логика генерации JSX
       }
   }
   ```
2. **Добавьте в NodeType.cs**

   ```csharp
   public enum NodeType
   {
       // ...
       NewNode,
   }
   ```
3. **Добавьте в проект**

   - Включите файл в jsxbin_to_jsx.csproj
   - Регистрация происходит автоматически в AbstractNode.InitializeDecoders()

### Стиль кода

#### C# стиль

- Используйте PascalCase для классов и методов
- Используйте camelCase для переменных
- Добавляйте XML документацию для публичных методов
- Следуйте Microsoft C# coding conventions

```csharp
/// <summary>
/// Decodes a binary expression from the JSXBIN stream
/// </summary>
public override void Decode()
{
    // Decode left operand
    var leftOperand = DecodeExpression();
  
    // Decode operator
    var op = DecodeOperator();
  
    // Decode right operand
    var rightOperand = DecodeExpression();
}
```

#### Тестирование

- Каждый новый узел должен иметь тесты
- Используйте AAA паттерн (Arrange, Act, Assert)
- Тестируйте граничные случаи

```csharp
[Test]
public void Decode_ValidBinaryExpression_ReturnsCorrectJsx()
{
    // Arrange
    var jsxbin = "binary_expression_data";
    var expected = "a + b";
  
    // Act
    var result = BinaryExpr.Decode(jsxbin);
  
    // Assert
    Assert.AreEqual(expected, result);
}
```

## 🧪 Тестирование

### Структура тестов

```
jsxbin_to_jsx.Tests/
├── Unit Tests/           # Тесты отдельных компонентов
├── Integration Tests/    # Тесты полного потока
└── Regression Tests/     # Тесты совместимости
```

### Запуск тестов

```bash
# Все тесты
dotnet test

# Конкретный тест
dotnet test --filter "TestMethodName"

# Покрытие кода
dotnet test --collect:"XPlat Code Coverage"
```

### Добавление тестов

#### Unit тесты для узлов

```csharp
[TestFixture]
public class BinaryExprTests
{
    [Test]
    public void Decode_AdditionExpression_ReturnsCorrectJsx()
    {
        // Тест сложения
    }
  
    [Test]
    public void Decode_MultiplicationExpression_ReturnsCorrectJsx()
    {
        // Тест умножения
    }
}
```

#### Интеграционные тесты

```csharp
[Test]
public void Decode_CompleteFile_ReturnsValidJsx()
{
    // Тест полного файла
}
```

## 📋 Pull Request процесс

### Перед отправкой PR

- [ ] Все тесты проходят
- [ ] Код следует стилю проекта
- [ ] Документация обновлена
- [ ] Commit сообщения следуют [Conventional Commits](https://conventionalcommits.org/)

### PR шаблон

```markdown
## Описание
Краткое описание изменений

## Тип изменений
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Тестирование
- [ ] Добавлены новые тесты
- [ ] Все тесты проходят
- [ ] Проверено вручную

## Чеклист
- [ ] Код следует стилю проекта
- [ ] Документация обновлена
- [ ] Нет breaking changes без предупреждения
```

## 🐛 Отчеты о багах

### Шаблон отчета

```markdown
## Описание проблемы
Четкое описание проблемы

## Воспроизведение
Шаги для воспроизведения:
1. Запустить команду `...`
2. Использовать файл `...`
3. Видеть ошибку

## Ожидаемое поведение
Что должно произойти

## Фактическое поведение
Что происходит на самом деле

## Окружение
- OS: Windows 10
- .NET Framework: 4.7.2
- Версия конвертера: 1.0.0

## Дополнительная информация
Логи, скриншоты, примеры файлов
```

## 💡 Идеи для улучшения

### Приоритетные задачи

- [ ] Поддержка .NET Core
- [ ] GUI интерфейс
- [ ] Улучшенная обработка ошибок
- [ ] Больше тестовых случаев

### Как предложить идею

1. Проверьте [существующие issues](https://github.com/yourusername/jsxbin-to-jsx-converter/issues)
2. Создайте discussion для обсуждения
3. Если идея одобрена — создайте issue

## 📞 Связь

- **GitHub Issues**: [Сообщить о проблеме](https://github.com/yourusername/jsxbin-to-jsx-converter/issues)
- **GitHub Discussions**: [Вопросы и обсуждения](https://github.com/yourusername/jsxbin-to-jsx-converter/discussions)
- **Email**: IMgalaxy.light@yandex.com

---

Спасибо за вклад! 🎉
