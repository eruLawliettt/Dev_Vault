#fundamentals 
[[Loops]]

Инструкция `while`

Оператор `while` выполняет оператор или блок операторов, пока определенное логическое выражение равно значению `true`. Так как это выражение оценивается перед каждым выполнением цикла, цикл `while` выполняется ноль или несколько раз. Цикл `while` отличается от `do` цикла, который выполняется один или несколько раз.

`while (timeInHours <= 10)`
`{`
    `Console.WriteLine($"Now {timeInHours} AM, Dima drunk on {dimaDrunkFrom0To10} of 10");`
    `timeInHours++;`

    if (dimaDrunkFrom0To10 == 5)
        continue;
        
    dimaDrunkFrom0To10++;
`}`