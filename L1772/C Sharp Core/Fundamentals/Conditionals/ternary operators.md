#fundamentals 
[[Conditionals]]

Условный оператор `?:`, также называемый тернарным, вычисляет логическое выражение и в зависимости от полученного значения `true` или `false` возвращает результат одного из двух соответствующих выражений, как показано в следующем примере.

`condition ? consequent : alternative`

`Dima.Drunk = true;`

`Dima.IsHappy = Dima.Drunk ? true : false;`

Выражение `condition` должно принимать значение `true` или `false`. Если `condition` принимает значение `true`, вычисляется выражение `consequent`, а результат становится результатом операции. Если `condition` принимает значение `false`, вычисляется выражение `alternative`, а результат становится результатом операции. Вычисляется только выражение `consequent` или `alternative`. Условные выражения являются целевыми типами. Это значит, что если известен целевой тип условного выражения, типы `consequent` и `alternative` должны быть неявно преобразованы в целевой тип.

//-----------------------------------------------------------------------------------------------

Тернарный оператор в C# вычисляет логическое выражение и в зависимости от полученного значения `true` или `false` возвращает результат одного из двух соответствующих выражений. 

**Общая форма тернарного оператора**: `condition ? consequent : alternative. 

Значение выражения определяется следующим образом: 

- Сначала вычисляется `condition`.
- Если оно истинно, то вычисляется `consequent`, а полученный результат определяет значение всего выражения в целом.
- Если же `condition` оказывается ложным, то вычисляется `alternative`, и его значение становится общим для всего выражения. 

**Примеры использования тернарного оператора**:

- Если все выражения относятся к типу `bool`, то такой оператор может заменить собой условное выражение в цикле или операторе `if`. 
- Значение, которое даёт оператор, можно использовать в качестве аргумента при вызове метода. 