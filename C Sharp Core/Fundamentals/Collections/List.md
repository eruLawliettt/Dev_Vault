#fundamentals 
[[Collections]]

`List<T> Класс`

Представляет строго типизированный список объектов, доступных по индексу. Поддерживает методы для поиска по списку, выполнения сортировки и других операций со списками.

`//Person.cs`
`public List<string> Beers { get; set; } = new List<string>();`

`//Program.cs`
`Dima.Beers.Add("Клянское");`
`Dima.Beers.Add("Мельник");`
`Dima.Beers.Add("Толкин Дэнс");`
`Dima.Beers.Add("ОХОТА");`
`Dima.Beers.Add("Боярыня");`

`Dima.Beers.ForEach(b => Console.WriteLine(b));`

`Console.WriteLine(Dima.Beers[2]);`