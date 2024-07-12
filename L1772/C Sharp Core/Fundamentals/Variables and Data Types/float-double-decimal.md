#fundamentals 
[[Variables and Data Types]]

Числовые типы с плавающей запятой представляют действительные числа. Все числовые типы с плавающей запятой являются [типами значений](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-types). Они также представляют собой [простые типы](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/value-types#built-in-value-types) и могут быть инициализированы [литералами](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types#real-literals). Все числовые типы с плавающей запятой поддерживают [арифметические](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/arithmetic-operators) операторы, а также операторы [сравнения](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/comparison-operators) и [равенства](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/operators/equality-operators).

`float` - дохуя.
`double` - чуть больше чем дохуя.
`decimal` - ещё больше чем дохуя вместе, точнее чем предыдущие дохуя, поэтому decimal используется везде, где фигурируют финансовые операции.

Суффиксом обозначается тип значения, для `float` - это F, для `double` это D, для `decimal` это M, по умолчанию, числовые типы с плавающей запятой являются `double`. 

float floatValue = 12.5F;
double doubleValue = 100.52D;
decimal decimalValue = 13370.12M;

Значение по умолчанию для типов `float-double-decimal` - 0.