#DeepCSharp 
[[Deep C Sharp]]

**Object и Collection Initializers в C#** — это удобный синтаксис для инициализации объектов и коллекций без явного вызова конструктора. Они делают код более читаемым и лаконичным. 

**Object Initializers** позволяют присваивать значения любым доступным полям или свойствам объекта во время его создания. При этом не нужно вызывать конструктор для каждого свойства. 

**Collection Initializers** позволяют кратко определить и заполнить коллекцию. Они могут использоваться с любым типом коллекции, который реализует IEnumerable и имеет метод Add. 

**Примеры использования**:

- **Список инициализаторов**: 
    `var numbers = new List<int> { 1, 2, 3, 4, 5 }`
- **Инициализаторы для словарей**: 
    `var capitals = new Dictionary<string, string> { { "USA", "Washington, D.C." }, { "UK", "London" }, { "France", "Paris" } }`


`var Shlyapa = new Rat() { Id = 2, Name = "Shlyapa" };`
`var listRats = new List<Rat>() { Dan, Shlyapa };`

`foreach(var item in listRats)`
`{`
    `Console.WriteLine(item.ToString());`
`}`
