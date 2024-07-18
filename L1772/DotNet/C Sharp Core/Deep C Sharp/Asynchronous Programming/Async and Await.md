#DeepCSharp 
[[Asynchronous Programming]]

Асинхронность позволяет вынести отдельные задачи из основного потока в специальные асинхронные методы и при этом более экономно использовать потоки. Асинхронные методы выполняются в отдельных потоках. Однако при выполнении продолжительной операции поток асинхронного метода возвратится в пул потоков и будет использоваться для других задач. А когда продолжительная операция завершит свое выполнение, для асинхронного метода опять выделяется поток из пула потоков, и асинхронный метод продолжает свою работу.

Ключевыми для работы с асинхронными вызовами в C# являются два оператора: async и await, цель которых - упростить написание асинхронного кода. Они используются вместе для создания асинхронного метода.

Асинхронный метод обладает следующими признаками:

- В заголовке метода используется модификатор async
    
- Метод содержит одно или несколько выражений await
    
- В качестве возвращаемого типа используется один из следующих:
    
    - `void`
        
    - `Task`
        
    - `Task<T>`
        
    - `ValueTask<T>`
        

Асинхронный метод, как и обычный, может использовать любое количество параметров или не использовать их вообще. Однако асинхронный метод не может определять параметры с модификаторами out, ref и in.

Также стоит отметить, что слово async, которое указывается в определении метода, НЕ делает автоматически метод асинхронным. Оно лишь указывает, что данный метод может содержать одно или несколько выражений await.

### Ключевое слово Async

Ключевое слово `async` используется для обозначения метода как асинхронного. Оно указывает, что метод может выполнять неблокирующую операцию и возвращать `Task` или `Task<TResult>` объект.

### Ключевое слово Await

Ключевое слово `await` используется в асинхронном методе, чтобы временно приостановить его выполнение и вернуть управление вызывающему методу до завершения ожидаемой задачи. Это позволяет тем временем продолжать выполнение других задач, гарантируя, что приложение остается отзывчивым.

`async Task<string> FetchDataAsync()`
`{`
    `using (var httpClient = new HttpClient())`
    `{`
        `string result = await httpClient.GetStringAsync("https://example.com/data");`

        return result;
    }
`}`

//-----------------------------------------------------------------------------------------------

 await ExecuteAsync();

 void Execute()
 {
     var watch = Stopwatch.StartNew();

     RunDownloadSync();

     watch.Stop();
     var elapsedMs = watch.ElapsedMilliseconds;
     Console.WriteLine("Execution time is " + elapsedMs);
 }

 async Task ExecuteAsync()
 {
     var watch = Stopwatch.StartNew();

     await RunDownloadParallelAsync();

     watch.Stop();
     var elapsedMs = watch.ElapsedMilliseconds;
     Console.WriteLine("Execution time is " + elapsedMs);
 }


 List<string> PrepData()
 {
     return ["https://www.yahoo.com",
 "https://www.google.com",
 "https://www.microsoft.com",
 "https://like-pizza.ru",
 "https://www.codeproject.com"];
 }

 void RunDownloadSync()
 {
     List<string> websites = PrepData();

     foreach (string site in websites)
     {
         WebsiteDataModel result = DownloadWebsite(site);
         string res = ReportWebsiteInfo(result);

         Console.WriteLine(res);
     }
 }

 async Task RunDownloadAsync()
 {
     List<string> websites = PrepData();

     foreach (string site in websites)
     {
         WebsiteDataModel result = await Task.Run(() => DownloadWebsite(site));
         Console.WriteLine(ReportWebsiteInfo(result));
     }
 }

 async Task RunDownloadParallelAsync()
 {
     List<string> websites = PrepData();
     List<Task<WebsiteDataModel>> tasks = new List<Task<WebsiteDataModel>>();

     foreach (string site in websites)
     {
         tasks.Add(Task.Run(() => DownloadWebsite(site)));             
     }

     var result = await Task.WhenAll(tasks);

     foreach (var item in result)
     {
         Console.WriteLine(ReportWebsiteInfo(item));
     }    
 }  

 WebsiteDataModel DownloadWebsite(string url)
 {
     using WebClient client = new();
     WebsiteDataModel website = new(url, client.DownloadString(url));

     return website;
 }

 string ReportWebsiteInfo(WebsiteDataModel data)
 {
     return $"{data.Url} downloaded: {data.Data.Length} characters long.{Environment.NewLine}";
 }



