#fundamentals 
[[Collections]]

`Dictionary<TKey, TValue> Класс`

Представляет коллекцию ключей и значений.
Параметры типа

`TKey`
Тип ключей в словаре.

`TValue`
Тип значений в словаре.

Наследование
`Object` -> `Dictionary<TKey,TValue>`

//-----------------------------------------------------------------------------------------------

`Dictionary<string, string> keyValuePairs = new();`

`keyValuePairs.Add("Расул", "Саня");`
`keyValuePairs.Add("Весёлая музыка", "Грустная музыка");`
`keyValuePairs.Add("Харт атак", "Чёт моторчик борохлит, надо покурить");`
`keyValuePairs.Add("Перестань говорить хуйню", "Ёбнем");`
`keyValuePairs.Add("Обычная пьянка", "Лучший день в жизни");`

`foreach (var pair in keyValuePairs)`
`{` 
    `Console.WriteLine(pair);`
`}`

`Console.WriteLine();`
`Console.WriteLine(keyValuePairs["Перестань говорить хуйню"]);`
`Console.WriteLine(keyValuePairs["Расул"]);`