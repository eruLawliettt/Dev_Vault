#fundamentals 
[[Fundamentals]]

Операторы итерации многократно выполняют инструкцию или блок инструкций. [Оператор](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-for-statement) `for` выполняет текст, пока указанное логическое выражение вычисляется`true`. [Инструкция](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-foreach-statement) `foreach` перечисляет элементы коллекции и выполняет его текст для каждого элемента коллекции. [Оператор](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-do-statement) `do` условно выполняет свой текст один или несколько раз. [Оператор](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/iteration-statements#the-while-statement) `while` условно выполняет его тело ноль или более раз.

В любой момент в тексте инструкции итерации можно выйти из цикла с помощью инструкции`break`. Вы можете перейти к следующей итерации в цикле с помощью инструкции`continue`.

[[for]]
[[foreach]]
[[do]]
[[while]]

//-----------------------------------------------------------------------------------------------

`break` - выводит из цикла

`foreach(var beer in Dima.Beers)`
`{`
    `if (beer == "ОХОТА")`
    `{`
        `Console.WriteLine("Ебать, Охота! ЁЁЁЁЁЁЁ");`
        `break;`
    `}`
        
`Console.WriteLine(beer);`
`}`

//-----------------------------------------------------------------------------------------------

`continue` - не даёт выполнять инструкции после условия, цикл идёт дальше

`int dimaDrunkFrom0To10 = 0;`
`int timeInHours = 0;`
`while (timeInHours <= 10)`
`{`
    `Console.WriteLine($"Now {timeInHours} AM, Dima drunk on {dimaDrunkFrom0To10} of 10");`
    `timeInHours++;`

`if (dimaDrunkFrom0To10 == 5)`
        `continue;`

`dimaDrunkFrom0To10++;`
`}`