#fundamentals 
[[Loops]]

Инструкция `foreach`

Оператор `foreach` выполняет оператор или блок операторов для каждого элемента в экземпляре типа, который реализует интерфейс `System.Collections.IEnumerable` или `System.Collections.Generic.IEnumerable<T>`, как показано в следующем примере.

`foreach(var beer in Dima.Beers)`
`{`
    `if (beer == "ОХОТА")`
    `{`
        `Console.WriteLine("Ебать, Охота! ЁЁЁЁЁЁЁ");`
        `break;`
    `}`
    `Console.WriteLine(beer);`
`}`