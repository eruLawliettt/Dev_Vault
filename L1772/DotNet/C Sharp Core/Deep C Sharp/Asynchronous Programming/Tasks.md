#DeepCSharp 
[[Asynchronous Programming]]

В эпоху многоядерных машин, которые позволяют параллельно выполнять сразу несколько процессов, стандартных средств работы с потоками в .NET уже оказалось недостаточно. Поэтому во фреймворк .NET была добавлена библиотека параллельных задач TPL (Task Parallel Library), основной функционал которой располагается в пространстве имен System.Threading.Tasks. Данная библиотека упрощает работу с многопроцессорными, многоядерными системами. Кроме того, она упрощает работу по созданию новых потоков. Поэтому обычно рекомендуется использовать именно TPL и ее классы для создания многопоточных приложений, хотя стандартные средства и класс Thread по-прежнему находят широкое применение.

В основе библиотеки TPL лежит концепция задач, каждая из которых описывает отдельную продолжительную операцию. В библиотеке классов .NET задача представлена специальным классом - классом Task, который находится в пространстве имен System.Threading.Tasks. Данный класс описывает отдельную задачу, которая запускается асинхронно в одном из потоков из пула потоков. Хотя ее также можно запускать синхронно в текущем потоке. Однако в любом случае следует отметить, что задача - это не поток.

Для определения и запуска задачи можно использовать различные способы.

//1
`Task task = new(delegate ()`
`{`
    `Console.WriteLine("New Task Hello!");`
    `Console.WriteLine(Thread.CurrentThread.Name);`
`});`
`task.Start();`

//2
`Task taskNew = Task.Factory.StartNew(() => Console.WriteLine("Task New Hello" + "\n" + Thread.CurrentThread.Name));`

//3
`Task taskRun = Task.Run(() => Console.WriteLine($"TaskRun Hello! \n{Thread.CurrentThread.Name}"));`

//-----------------------------------------------------------------------------------------------

`task.Wait();` останавливает текущий поток в ожидании завершения `task` задачи

//-----------------------------------------------------------------------------------------------

### Свойства класса Task

Класс Task имеет ряд свойств, с помощью которых мы можем получить информацию об объекте. Некоторые из них:

- AsyncState: возвращает объект состояния задачи
    
- CurrentId: возвращает идентификатор текущей задачи (статическое свойство)
    
- Id: возвращает идентификатор текущей задачи
    
- Exception: возвращает объект исключения, возникшего при выполнении задачи
    
- Status: возвращает статус задачи. Представляет перечисление `System.Threading.Tasks.TaskStatus`, которое имеет следующие значения:
    
    - `Canceled`: задача отменена
        
    - `Created`: задача создана, но еще не запущена
        
    - `Faulted`: в процессе работы задачи произошло исключение
        
    - `RanToCompletion`: задача успешно завершена
        
    - `Running`: задача запущена, но еще не завершена
        
    - `WaitingForActivation`: задача ожидает активации и постановки в график выполнения
        
    - `WaitingForChildrenToComplete`: задача завершена и теперь ожидает завершения прикрепленных к ней дочерних задач
        
    - `WaitingToRun`: задача поставлена в график выполнения, но еще не начала свое выполнение
        
- IsCompleted: возвращает true, если задача завершена
    
- IsCanceled: возвращает true, если задача была отменена
    
- IsFaulted: возвращает true, если задача завершилась при возникновении исключения
    
- IsCompletedSuccessfully: возвращает true, если задача завершилась успешно

//-----------------------------------------------------------------------------------------------

Если необходимо завершить выполнение программы или вообще выполнять некоторый код лишь после того, как все задачи из массива завершатся, то применяется метод `Task.WaitAll(tasks)`

Также мы можем применять метод `Task.WaitAny(tasks)`. Он ждет, пока завершится хотя бы одна из массива задач.

//-----------------------------------------------------------------------------------------------

`string R = "Russel";`
`string A = "Alex";`
`string m = "look what i found, alex! u will be shoked! OMG! follow this --->> AmazingGayWebsite.com";`

`Task<string> sendTask = new(() => SendMessage(R, A, m));`
`sendTask.Start();`
`string StolenMessage = sendTask.Result;`

`Console.WriteLine($"!!!ОБНАРОДОВАНО СЕКРЕТНОЕ ПИСЬМО ГЛАВ КОМПАНИИ KUSMANOV!!!");`
`Console.WriteLine(StolenMessage);`

`string SendMessage(string sender, string recipient, string message) => $"{sender} отправил письмо {recipient}, содержание письма: {message}";`

//-----------------------------------------------------------------------------------------------

Первая задача задается с помощью лямбда-выражения, которое просто выводит id этой задачи. Вторая задача - задача продолжения задается с помощью метода ContinueWith, который в качестве параметра принимает делегат `Action<Task>`. То есть метод PrintTask, который передается в вызов ContinueWith, должен принимать параметр типа Task.

`string R = "Russel";`
`string A = "Alex";`
`string m = "look what i found, alex! u will be shoked! OMG! follow this --->> AmazingGayWebsite.com";`

`Task<string> sendTask = new(() => SendMessage(R, A, m));`
`sendTask.Start();`

`Task zhulikTask = sendTask.ContinueWith(task => StealMessage(task.Result));`

`string SendMessage(string sender, string recipient, string message)` 
    `=> $"{sender} отправил письмо {recipient}, содержание письма: {message}";`

`void StealMessage(string mes)`
`{`
    `Console.WriteLine($"!!!ОБНАРОДОВАНО СЕКРЕТНОЕ ПИСЬМО ГЛАВ КОМПАНИИ KUSMANOV!!!");`
    `Console.WriteLine(mes);`
`}`

//-----------------------------------------------------------------------------------------------

Класс Parallel также является частью TPL и предназначен для упрощения параллельного выполнения кода. Parallel имеет ряд методов, которые позволяют распараллелить задачу.

`Parallel.Invoke(`
    `() =>`
    `{`
        `Thread.Sleep(300);`
        `Console.WriteLine(Thread.CurrentThread.Name + " Выполняется действие 1.");` 
    `},`
    `Print,`
    `() => { Console.WriteLine(3); }` 
 `);`
 
`Parallel.For`
Метод Parallel.For позволяет выполнять итерации цикла параллельно. Он имеет следующее определение:

`For(int, int, Action<int>)`
Первый параметр метода задает начальный индекс элемента в цикле, а второй параметр - конечный индекс. Третий параметр - делегат Action - указывает на метод, который будет выполняться один раз за итерацию:

`Parallel.For(1, 5, Square);`

`// вычисляем квадрат числа`
`void Square(int n)`
`{`
    `Console.WriteLine($"Выполняется задача {Task.CurrentId}");`
    `Console.WriteLine($"Квадрат числа {n} равен {n * n}");`
`}`

`Parallel.ForEach`
Метод Parallel.ForEach осуществляет итерацию по коллекции, реализующей интерфейс IEnumerable, подобно циклу foreach, только осуществляет параллельное выполнение перебора. Он имеет следующее определение:

`ParallelLoopResult ForEach<TSource>(IEnumerable<TSource> source, Action<TSource> body)`
где первый параметр представляет перебираемую коллекцию, а второй параметр - делегат, выполняющийся один раз за итерацию для каждого перебираемого элемента коллекции.

На выходе метод возвращает структуру `ParallelLoopResult`, которая содержит информацию о выполнении цикла.

`Parallel.ForEach<int>(`
    `[1, 3, 5, 8],`
    `Square );`

`void Square(int n)`
    `{`
    `Console.WriteLine($"Выполняется задача {Task.CurrentId}");`
    `Console.WriteLine($"Квадрат числа {n} равен {n * n}");`
    `Thread.Sleep(1000);`
`}

Выход из цикла

В стандартных циклах for и foreach предусмотрен преждевременный выход из цикла с помощью оператора `break`. В методах Parallel.ForEach и Parallel.For мы также можем, не дожидаясь окончания цикла, выйти из него

`ParallelLoopResult result = Parallel.For(`
    `1, 13,`
    `Square );`

`if (!result.IsCompleted)`
`{`
    `Console.WriteLine($"Выполнение цикла завершено на итерации {result.LowestBreakIteration}");`
`}`

`void Square(int n, ParallelLoopState state)`
    `{`
    `if (n == 5)`
    `{`
        `state.Break();`
    `}`

    Console.WriteLine($"Выполняется задача {Task.CurrentId}");
    Console.WriteLine($"Квадрат числа {n} равен {n * n}");
    Thread.Sleep(1000);`
`}`

//-----------------------------------------------------------------------------------------------

Параллельное выполнение задач может занимать много времени. И иногда может возникнуть необходимость прервать выполняемую задачу. Для этого платформа .NET предоставляет структуру CancellationToken из пространства имен System.Threading.

Общий алгоритм отмены задачи обычно предусматривает следующий порядок действий:

Создание объекта CancellationTokenSource, который управляет и посылает уведомление об отмене токену.

С помощью свойства CancellationTokenSource.Token получаем собственно токен - объект структуры CancellationToken и передаем его в задачу, которая может быть отменена.

CancellationTokenSource cancelTokenSource = new CancellationTokenSource(); 
CancellationToken token = cancelTokenSource.Token;
Для передачи токена в задачу можно применять один из конструкторов класса Task:

CancellationTokenSource cancelTokenSource = new CancellationTokenSource(); 
CancellationToken token = cancelTokenSource.Token;
Task task = new Task(() => { выполняемые_действия}, token); //
Определяем в задаче действия на случай ее отмены.

Вызываем метод CancellationTokenSource.Cancel(), который устанавливает для свойства CancellationToken.IsCancellationRequested значение true. Стоит понимать, что сам по себе метод CancellationTokenSource.Cancel() не отменяет задачу, он лишь посылает уведомление об отмене через установку свойства CancellationToken.IsCancellationRequested. Каким образом будет происходить выход из задачи, это решает сам разработчик.

Класс CancellationTokenSource реализует интерфейс IDisposable. И когда работа с объектом CancellationTokenSource завершена, у него следует вызвать метод Dispose для освобождения всех связанных с ним используемых ресурсов. (Вместо явного вызова метода Dispose можно использовать конструкцию using).

Теперь касательно третьего пункта - определения действий отмены задачи. Как именно завершить задачу? Конкретные действия на лежат целиком на разработчике, тем не менее есть два общих варианта выхода:

При получении сигнала отмены выйти из метода задачи, например, с помощью оператора return или построив логику метода соответствующим образом. Но следует учитывать, что в этом случае задача перейдет в состояние TaskStatus.RanToCompletion, а не в состояние TaskStatus.Canceled.

При получении сигнала отмены сгенерировать исключение OperationCanceledException, вызвав у токена метод ThrowIfCancellationRequested(). После этого задача перейдет в состояние TaskStatus.Canceled.

//-----------------------------------------------------------------------------------------------

//soft
`using (CancellationTokenSource cancellationTokenSource = new())`
`{`
    `CancellationToken cancellationToken = cancellationTokenSource.Token;`

    Task task = new(() =>
    {
        for (int i = 0; i < 10; i++)
        {
            if(cancellationToken.IsCancellationRequested)
            {
                Console.WriteLine("Операция прервана!!!");
                return;
            }
            else
            {
                Console.WriteLine($"Квадрат числа {i} равен {i * i}");
                Thread.Sleep(200);
            }
        }
    }, cancellationToken);

    task.Start();

    Thread.Sleep(1000);
    cancellationTokenSource.Cancel();
    Thread.Sleep(1000);
    Console.WriteLine($"Task status: {task.Status}");
`}`

//hard
`using (CancellationTokenSource cancellationTokenSource = new())`
`{`
    `CancellationToken cancellationToken = cancellationTokenSource.Token;`
    
    Task task = new(() =>
    {
        for (int i = 1; i < 101; i++)
        {
            cancellationToken.ThrowIfCancellationRequested();

            Console.WriteLine($"Loading: {i}%");
            Thread.Sleep(100);
            
        }
    }, cancellationToken);

    try
    {
        task.Start();
        Thread.Sleep(1000);
        cancellationTokenSource.Cancel();

        task.Wait();
    }
    catch (AggregateException ae)
    {
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine(ex.Message);
        }
    }
    Console.WriteLine($"Task status: {task.Status}");
`}`

![[Pasted image 20240714144206.png]]