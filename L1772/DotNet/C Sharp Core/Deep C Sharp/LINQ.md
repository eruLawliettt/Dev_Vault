#DeepCSharp 
[[Deep C Sharp]]

LINQ (Language-Integrated Query) представляет простой и удобный язык запросов к источнику данных. В качестве источника данных может выступать объект, реализующий интерфейс IEnumerable (например, стандартные коллекции, массивы), набор данных DataSet, документ XML. Но вне зависимости от типа источника LINQ позволяет применить ко всем один и тот же подход для выборки данных.

Существует несколько разновидностей LINQ:

- LINQ to Objects: применяется для работы с массивами и коллекциями
    
- LINQ to Entities: используется при обращении к базам данных через технологию Entity Framework
    
- LINQ to XML: применяется при работе с файлами XML
    
- LINQ to DataSet: применяется при работе с объектом DataSet
    
- Parallel LINQ (PLINQ): используется для выполнения параллельных запросов


`string[] people = ["Tom", "Bob", "Sam", "Tim", "Tomas", "Bill"];`

`// создаем новый список для результатов`
`var selectedPeople = new List<string>();`
`// проходим по массиву`
`foreach (string person in people)`
`{`
    `// если строка начинается на букву T, добавляем в список`
    `if (person.ToUpper().StartsWith("T"))`
        `selectedPeople.Add(person);`
`}`
`// сортируем список`
`selectedPeople.Sort();`

`foreach (string person in selectedPeople)`
    `Console.WriteLine(person);`

### Операторы запросов LINQ

Операторы запросов LINQ в каком-то роде частично напоминают синтаксис запросов SQL, поэтому если вы работали когда-нибудь с sql-запросами, то будет проще понять общую концепцию. Итак, изменим предыдущий пример, применив операторы запросов LINQ:

`string[] people = { "Tom", "Bob", "Sam", "Tim", "Tomas", "Bill" };`


`var selectedPeople = from p in people` 
                     `where p.ToUpper().StartsWith("T")`
                     `orderby p`
                     `select p;`

`foreach (string person in selectedPeople)`
    `Console.WriteLine(person);`

### Методы расширения LINQ

Кроме стандартного синтаксиса `from .. in .. select` для создания запроса LINQ мы можем применять специальные методы расширения, которые определены для интерфейса `IEnumerable`. Как правило, эти методы реализуют ту же функциональность, что и операторы LINQ типа `where` или `orderby`.

`string[] people = { "Tom", "Bob", "Sam", "Tim", "Tomas", "Bill" };`

`var selectedPeople = people.Where(p => p.ToUpper().StartsWith("T")).OrderBy(p => p);`

`foreach (string person in selectedPeople)`
    `Console.WriteLine(person);`


`Person[] list = [`
    `new Person("Alex", 19),` 
    `new Person("Russel", 29),` 
    `new Person("Dima Nedovodnenko", 9),`
    `new Person("Dima Nedopivchenko", 25),`
    `new Person("Dima Stariychelchenko", 75) ];`

`var names = list.Select(p => p.name);`

`foreach(var name in names)`
    `Console.WriteLine(name);` 

#так_можно_но_нихуя_не_нужно 
Переменые в запросах и оператор `let`

