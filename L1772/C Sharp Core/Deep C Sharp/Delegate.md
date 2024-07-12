#DeepCSharp 
[[Deep C Sharp]]

Делегат — это тип, который представляет ссылки на методы с определенным списком параметров и типом возвращаемого значения. При создании экземпляра делегата этот экземпляр можно связать с любым методом с совместимой сигнатурой и типом возвращаемого значения. Метод можно вызвать (активировать) с помощью экземпляра делегата.

Делегаты используются для передачи методов в качестве аргументов к другим методам. Обработчики событий — это ничто иное, как методы, вызываемые с помощью делегатов. При создании пользовательского метода класс (например, элемент управления Windows) может вызывать этот метод при появлении определенного события.

`static int Sum(int a, int b) => a + b;`
`static int Multiply(int a, int b) => a * b;`

`static void Hello() => Console.WriteLine("Hello!");`
`static void Wazzup() => Console.WriteLine("Wazzup black bro!");`

`int a = 5;`
`int b = 10;`

`IntOperator delOperator;`
`delOperator = Sum;`
`delOperator += Multiply;`
`Console.WriteLine(delOperator(a, b));`
`//50` 

`Hi mes;`
`mes = Hello;`
`mes += Wazzup;`
`mes?.Invoke();`
`//Hello!`
`//Wazzup black bro!`

`Hi mes2 = Hello;`
`Hi mes3 = mes + mes2;`
`mes3();`
`//Hello!`
`//Wazzup black bro!`
`//Hello!`

`delegate int IntOperator(int a, int b);`
`delegate void Hi();`

`delegate T Oper<T, K, F>(K Kvalue, F Fvalue);`

//-----------------------------------------------------------------------------------------------

`DoOperation(5, 4, Add);`         
`DoOperation(5, 4, Subtract);`    
`DoOperation(5, 4, Multiply);`    

`void DoOperation(int a, int b, Operation op)`
`{`
    `Console.WriteLine(op(a, b));`
`}`

`int Add(int x, int y) => x + y;`
`int Subtract(int x, int y) => x - y;`
`int Multiply(int x, int y) => x * y;`

`delegate int Operation(int x, int y);`

//-----------------------------------------------------------------------------------------------

`Operation operation = SelectOperation(OperationType.Add);`
`Console.WriteLine(operation(10, 4));    // 14`

`operation = SelectOperation(OperationType.Subtract);`
`Console.WriteLine(operation(10, 4));    // 6`

`operation = SelectOperation(OperationType.Multiply);`
`Console.WriteLine(operation(10, 4));    // 40`

`Operation SelectOperation(OperationType opType)`
`{`
    `switch (opType)`
    `{`
    `case OperationType.Add: return Add;`
    `case OperationType.Subtract: return Subtract;`
    `default: return Multiply;`
    `}`
`}`

`int Add(int x, int y) => x + y;`
`int Subtract(int x, int y) => x - y;`
`int Multiply(int x, int y) => x * y;`

`enum OperationType`
`{`
    `Add,` 
    `Subtract,` 
    `Multiply`
`}`

`delegate int Operation(int x, int y);`

//-----------------------------------------------------------------------------------------------

Hаиболее сильная сторона делегатов состоит в том, что они позволяют делегировать выполнение некоторому коду извне. И на момент написания программы мы можем не знать, что за код будет выполняться. Мы просто вызываем делегат. А какой метод будет непосредственно выполняться при вызове делегата, будет решаться потом.

Account.cs
`internal delegate void AccountHandler(string message);`
`internal class Account`
`{`
    `private int _sum;`
    `private AccountHandler? _taken;

    public int Sum
    {
        get { return _sum; }
        set { _sum = value; }
    }

    public Account(int sum)
    {
        _sum = sum;
    }
    
    public void RegisterHandler(AccountHandler handler)
    {
        _taken += handler;
    }

    public void UnregisterHandler(AccountHandler handler)
    {
        _taken -= handler;
    }

    public void Add(int sum)
    {
        _sum += sum;
    }
    
    public void Take(int sum)
    {
        if (_sum > sum) 
        {
            _sum -= sum;
            _taken?.Invoke($"Со счёта было списано {sum} денег.");
        }
        else
        {
            _taken?.Invoke($"Недостаточно средств. Баланс: {_sum}");
        }
    }
`}`

Program.cs
`Account account = new(300);`

`account.RegisterHandler(Notification);`
`account.RegisterHandler(GayNotification);`

`account.Take(150);`
`//code`

`account.UnregisterHandler(GayNotification);`
`account.Take(200);`
`//code`

`account.Take(30);`

`static void Notification(string str) => Console.WriteLine(str);`
`static void GayNotification(string str)`
`{`
    `Console.ForegroundColor = ConsoleColor.Green;`
    `Console.WriteLine(str);`
    `Console.ResetColor();`
`}`

Хотя в примере наш делегат принимал адрес на один метод, в действительности он может указывать сразу на несколько методов. Кроме того, при необходимости мы можем удалить ссылки на адреса определенных методов, чтобы они не вызывались при вызове делегата.
