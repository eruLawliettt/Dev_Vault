#DeepCSharp 
[[Deep C Sharp]]

- Быстрый ответ
    
- **Сериализация** — это процесс преобразования какого-либо объекта в поток байтов. После преобразования поток байтов можно записать на диск или сохранить в памяти.
    
    Для сериализации объектов в .NET можно использовать следующие форматы:
    
    - бинарный;
        
    - SOAP;
        
    - XML;
        
    - JSON.
        
    
    Для каждого формата предусмотрен свой класс:
    
    - для сериализации в бинарный формат — класс BinaryFormatter;
        
    - для формата SOAP — класс SoapFormatter;
        
    - для XML — XmlSerializer;
        
    - для JSON — DataContractJsonSerializer.

JSON (JavaScript Object Notation) является одним из наиболее популярных форматов для хранения и передачи данных. И платформа .NET предоставляет функционал для работы с JSON.

Основная функциональность по работе с JSON сосредоточена в пространстве имен System.Text.Json. Ключевым типом является класс JsonSerializer, который и позволяет сериализовать объект в json и, наоборот, десериализовать код json в объект C#.

Для сохранения объекта в json в классе JsonSerializer определен статический метод Serialize() и его асинхронный двойник SerializeAsyc().

Для десериализации кода json в объект C# применяется метод Deserialize() и его асинхронный двойник DeserializeAsync().

`string json = JsonSerializer.Serialize(GayBot);`
`Console.WriteLine(json);`

`Robot? restoredPerson = JsonSerializer.Deserialize<Robot>(json);`
`Console.WriteLine(restoredPerson?.GunType);`

`using (FileStream fs = new("bot.json", FileMode.OpenOrCreate))`
`{`
    `await JsonSerializer.SerializeAsync(fs, GayBot);`
    `Console.WriteLine("Data Saved");`
`}`

`using(FileStream fs = new("bot.json", FileMode.OpenOrCreate))`
`{`
    `Robot? robot = await JsonSerializer.DeserializeAsync<Robot>(fs);`
    `Console.WriteLine(robot?.GunType);`
`}`

### Настройка сериализации с помощью JsonSerializerOptions

По умолчанию JsonSerializer сериализует объекты в минимифицированный код. С помощью дополнительного параметра типа JsonSerializerOptions можно настроить механизм сериализации/десериализации, используя свойства JsonSerializerOptions. Некоторые из его свойств:

- AllowTrailingCommas: устанавливает, надо ли добавлять после последнего элемента в json запятую. Если равно `true`, запятая добавляется
    
- DefaultIgnoreCondition: устанавливает, будут ли сериализоваться/десериализоваться в json свойства со значениями по умолчанию
    
- IgnoreReadOnlyProperties: аналогично устанавливает, будут ли сериализоваться свойства, предназначенные только для чтения
    
- WriteIndented: устанавливает, будут ли добавляться в json пробелы (условно говоря, для красоты). Если равно `true` устанавливаются дополнительные пробелы

`var options = new JsonSerializerOptions()`
`{`
    `WriteIndented = true,`
`};`