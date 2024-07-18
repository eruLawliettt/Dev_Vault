#DeepCSharp 
[[Deep C Sharp]]

Блок [try](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/exception-handling-statements#the-try-statement) используется программистами C# для разбиения на разделы кода, который может затрагиваться исключением. Связанные с ним блоки [catch](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/exception-handling-statements#the-try-catch-statement) используются для обработки возможных исключений. Блок [finally](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/exception-handling-statements#the-try-finally-statement) содержит код, выполняемый вне зависимости от того, вызывается ли исключение в блоке `try`, например для освобождения ресурсов, выделенных в блоке `try`. Блоку `try` требуется один или несколько связанных блоков `catch` или блок `finally` (либо и то, и другое).

`Console.WriteLine("Start");`

`dynamic num = "13";`

`try`
`{`
    `Console.WriteLine(num++);`
`}`
`catch (Exception ex)`
`{`
    `Console.WriteLine(ex.Message);`
`}`
`finally`
`{`
    `Console.WriteLine("Finally");`
`}`

`Console.WriteLine("End");`

![[Pasted image 20240718161939.png]]