#fundamentals 
[[Variables and Data Types]]

Ключевое слово типа `bool` — это псевдоним для типа структуры [System.Boolean](https://learn.microsoft.com/ru-ru/dotnet/api/system.boolean) .NET, представляющий логическое значение: `true` или `false`.

Для выполнения логических операций со значениями типа `bool` используйте [логические](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/boolean-logical-operators) операторы. Тип `bool` является типом результата операторов [сравнения](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/comparison-operators) и [равенства](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/equality-operators). Выражение `bool` может быть управляющим условным выражением в операторах [if](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/selection-statements#the-if-statement), [do](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-do-statement), [while](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-while-statement) и [for](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-for-statement) и [условном операторе `?:`](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/conditional-operator).

bool value = true;

if (value) {
//do smth
}

Значение по умолчанию для типа `bool` - `false`.

