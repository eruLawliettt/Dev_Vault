#DeepCSharp 
[[Deep C Sharp]]

**Enum в C# — это тип значения, определённый набором логически связанных констант**. Он представляет собой набор символьных имён, связанных с уникальными целочисленными значениями. 

**Чтобы определить тип перечисления, используется оператор enum**: 

- После оператора enum указывается имя создаваемого типа. 
- Через двоеточие можно указать тип констант перечисления (должен быть целочисленным). Если не указывать тип явно, то будет использован int. 
- После этого приводится список символьных констант через запятую. 

**Примеры типов перечислений:**

`enum TypeOS {Windows, Linux, MacOS, Android}`

`enum WeekDay {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday}`

**С элементами типа перечисления можно производить различные операции**: приведение значения к целочисленному типу, операции сравнения, арифметические операции и другие.

`DayTime now = DayTime.Evening;`
`PrintMessage(now);`                   `// Добрый вечер`
`PrintMessage(DayTime.Afternoon);`    `// Добрый день`
`PrintMessage(DayTime.Night);`        `// Доброй ночи`

`void` `PrintMessage(DayTime dayTime)`
`{`
    `switch` `(dayTime)`
    `{`
        `case` `DayTime.Morning:`
            `Console.WriteLine("Доброе утро");`
            `break;`
        `case` `DayTime.Afternoon:`
            `Console.WriteLine("Добрый день");`
            `break;`
        `case` `DayTime.Evening:`
            `Console.WriteLine("Добрый вечер");`
            `break;
        `case` `DayTime.Night:`
            `Console.WriteLine("Доброй ночи");`
            `break;`
    `}`
`}`

`enum` `DayTime`
`{`
    `Morning,`
    `Afternoon,`
    `Evening,`
    `Night`
`}`

//-----------------------------------------------------------------------------------------------

`int n4 = 5;`

`Console.WriteLine($"Существует ли элемент под номером {n4} в перечислении: {Enum.IsDefined(enumType, n4)}");`