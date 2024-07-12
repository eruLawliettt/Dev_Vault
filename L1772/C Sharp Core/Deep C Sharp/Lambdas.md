#DeepCSharp 
[[Deep C Sharp]]

**Лямбда-выражения в C#** — это упрощённая запись анонимных методов. Они позволяют создать ёмкие лаконичные методы, которые могут возвращать некоторое значение и которые можно передать в качестве параметров в другие методы.

Ламбда-выражения имеют следующий синтаксис: слева от лямбда-оператора `=>` определяется список параметров, а справа блок выражений, использующий эти параметры:

`(список_параметров) => выражение`

С точки зрения типа данных лямбда-выражение представляет делегат. Например, определим простейшее лямбда-выражение:

1 реализация:
`Message hello = () => Console.WriteLine("Hello");`

2 реализация:
`Message hello = delegate`
`{`
    `Console.WriteLine("Hello");`
`};`

`hello();       // Hello`
`hello();       // Hello`
`hello();       // Hello`

`delegate void Message();`

В данном случае переменная hello представляет делегат Message - то есть некоторое действие, которое ничего не возвращает и не принимает никаких параметров. В качестве значения этой переменной присваивается лямбда-выражение. Это лямбда-выражение должно соответствовать делегату Message - оно тоже не принимает никаких параметров, поэтому слева от лямбда-оператора идут пустые скобки. А справа от лямбда-оператора идет выполняемое выражение - `Console.WriteLine("Hello")`

Затем в программе можно вызывать эту переменную как метод.

Если лямбда-выражение содержит несколько действий, то они помещаются в фигурные скобки:

`Message helloWorld = () =>`
`{`
    `Console.Write("Hello ");`
    `Console.WriteLine("World");`
`};`

`helloWorld();       // Hello World`

Выше мы определили переменную hello, которая представляет делегат Message. Но начиная с версии C# 10 мы можем применять неявную типизацию (определение переменной с помощью оператора var) при определении лямбда-выражения:


`var hello = () => Console.WriteLine("Hello");`
`hello();       // Hello`
`hello();       // Hello`
`hello();       // Hello`

Но какой тип в данном случае представляет переменная hello? При неявной типизации компилятор сам пытается сопоставить лямбда-выражение на основе его опеределения с каким-нибудь делегатом. Например, выше определенное лямбда-выражение hello по умолчанию компилятор будет рассматривать как переменную встроенного делегата Action, который не принимает никаких параметров и ничего не возвращает.

//-----------------------------------------------------------------------------------------------

Параметры лямбды
При определении списка параметров мы можем не указывать для них тип данных:

`Operation sum = (x, y) => Console.WriteLine($"{x} + {y} = {x + y}");`
`sum(1, 2);       // 1 + 2 = 3`
`sum(22, 14);    // 22 + 14 = 36`

`delegate void Operation(int x, int y);`

В данном случае компилятор видит, что лямбда-выражение sum представляет тип Operation, а значит оба параметра лямбды представляют тип int. Поэтому никак проблем не возникнет.

Однако если мы применяем неявную типизацию, то у компилятора могут возникнуть трудности, чтобы вывести тип делегата для лямбда-выражения, например, в следующем случае
`
`var sum = (x, y) => Console.WriteLine($"{x} + {y} = {x + y}"); // ! Ошибка
В этом случае можно указать тип параметров


`var sum = (int x, int y) => Console.WriteLine($"{x} + {y} = {x + y}");`
`sum(1, 2);       // 1 + 2 = 3`
`sum(22, 14);    // 22 + 14 = 36`

Если лямбда имеет один параметр, для которого не требуется указывать тип данных, то скобки можно опустить:


`PrintHandler print = message => Console.WriteLine(message);`
`print("Hello");         // Hello`
`print("Welcome");       // Welcome`

`delegate void PrintHandler(string message);`

//-----------------------------------------------------------------------------------------------
#CSharp12Feature 
Начиная с C# 12 параметры лямбда-выражений могут иметь значения по умолчанию:

`var welcome = (string message = "hello") => Console.WriteLine(message);`

`welcome?.Invoke(); // hello`
`welcome?.Invoke("HI Raisel!"); // HI Raisel!`
//-----------------------------------------------------------------------------------------------

Возвращение результата
Лямбда-выражение может возвращать результат. Возвращаемый результат можно указать после лямбда-оператора:


`var sum = (int x, int y) => x + y;`
`int sumResult = sum(4, 5);                  // 9`
`Console.WriteLine(sumResult);               // 9`

`Operation multiply = (x, y) => x * y;`
`int multiplyResult = multiply(4, 5);        // 20`
`Console.WriteLine(multiplyResult);          // 20`

`delegate int Operation(int x, int y);`

Если лямбда-выражение содержит несколько выражений (или одно выражение в фигурных скобках), тогда нужно использовать оператор return, как в обычных методах:

`var subtract = (int x, int y) =>`
`{`
    `if (x > y) return x - y;`
    `else return y - x;`
`};`
`int result1 = subtract(10, 6);  // 4` 
`Console.WriteLine(result1);     // 4`

`int result2 = subtract(-10, 6);  // 16`
`Console.WriteLine(result2);      // 16`



`Operation sum = (x, y) => x + y;`
`Console.WriteLine(sum(1, 2));`      
`Console.WriteLine(sum(22, 14));`  

`delegate int Operation(int x, int y);`

//-----------------------------------------------------------------------------------------------

Добавление и удаление действий в лямбда-выражении
Поскольку лямбда-выражение представляет делегат, тот как и в делегат, в переменную, которая представляет лямбда-выражение можно добавлять методы и другие лямбды:

`Action? helloo = () => Console.WriteLine("AmazingGayWebsite.com");`
`Action? message = () => Console.Write("Hello ");`

`message += () => Console.WriteLine("World"); // добавляем анонимное лямбда-выражение`
`message += helloo;   // добавляем лямбда-выражение из переменной hello`
`message += Print;   // добавляем метод`

`message?.Invoke();`

`Console.WriteLine("--------------"); // для разделения вывода`

`message -= Print;   // удаляем метод`
`message -= helloo;   // удаляем лямбда-выражение из переменной hello`

`message?.Invoke();  // на случай, если в message больше нет действий`

`void Print() => Console.WriteLine("Welcome to C#");`

//-----------------------------------------------------------------------------------------------

### Лямбда-выражение как аргумент метода

Как и делегаты, лямбда-выражения можно передавать параметрам метода, которые представляют делегат:

`int[] integers = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };`

`// найдем сумму чисел больше 5`
`int result1 = Sum(integers, number => number > 5);`

`Console.WriteLine(result1); // 30`

`// найдем сумму четных чисел`
`int result2 = Sum(integers, x => x % 2 == 0);`
`Console.WriteLine(result2);  //20`

`// number => number > 5`
`bool BiggerThanFive(int number)`
`{`
    `if (number > 5)`
        `return true;`
    `else`
        `return false;`
`}`

`// x => x % 2 == 0`
`bool IsEven(int number)`
`{`
    `if (number % 2 == 0)`
        `return true;`
    `else`
        `return false;`
`}`

`int Sum(int[] numbers, IsEqual func)`
`{`
    `int result = 0;`
    `foreach (int i in numbers)`
    `{`
        `if (func(i))`
            `result += i;`
    `}`
    `return result;`
`}`

`delegate bool IsEqual(int x);`

//-----------------------------------------------------------------------------------------------

### Лямбда-выражение как результат метода

Метод также может возвращать лямбда-выражение. В этом случае возвращаемым типом метода выступает делегат, которому соответствует возвращаемое лямбда-выражение. Например:

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
    `case OperationType.Add: return (x, y) => x + y;`

    case OperationType.Subtract: return (x, y) => x - y;

    default: return (x, y) => x * y;
    }
`}`

`enum OperationType`
`{`
    `Add,` 
    `Subtract,` 
    `Multiply`
`}`

`delegate int Operation(int x, int y);`

В данном случае метод SelectOperation() в качестве параметра принимает перечисление типа OperationType. Это перечисление хранит три константы, каждая из которых соответствует определенной арифметической операции. И в самом методе в зависимости от значения параметра возвращаем определенное лямбда-выражение.