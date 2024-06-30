#ObjectOrientedProgramming 
[[Encapsulation]]

**Record в C# — это специальный тип классов, который предоставляет неизменяемость и сравнение на основе значений**.
**Зачем нужны записи**:

- **Упрощают создание типов данных**. Записи обеспечивают лучшую безопасность при работе с ними. 
- **Подходят для моделирования типов данных**, таких как дата, время или координаты. 
- **Автоматически генерируют методы**, например, Equals, GetHashCode и ToString. 

По умолчанию записи являются **неизменяемыми объектами**. Для модификации значения любого свойства необходимо создать копию исходного экземпляра. Это предотвращает случайные изменения состояния и упрощает понимание и отладку кода.

Для объявления записи используется ключевое слово record.

`var person1 = new Person("Tom");`
`var person2 = new Person("Tom");`
`Console.WriteLine(p.Equals(person2)); // true`

`var user1 = new User("Tom");`
`var user2 = new User("Tom");`
`Console.WriteLine(user1.Equals(user2)); // false`

`public record Person`
`{`
    `public string Name { get; init; }`
    `public Person(string name) => Name = name;`
`}`

`public class User`
`{`
    `public string Name { get; init; }`
    `public User(string name) => Name = name;`
`}`

### Оператор with

В отличие от классов records поддерживают инициализацию с помощью оператора with. Он позволяет создать одну record на основе другой record:

`var tom = new Person("Tom", 37);`
`var sam = tom with { Name = "Sam" };`
`Console.WriteLine($"{sam.Name} - {sam.Age}"); // Sam - 37`
 
`public record Person`
`{`
    `public string Name { get; init; }`
    `public int Age { get; init; }`
    `public Person(string name, int age)`
    `{`
        `Name = name;`
        `Age = age;`
    `}`
`}`

После record, значения которой мы хотим скопировать, указывается оператор with, после которого в фигурных скобках указываются значения для тех свойств, которые мы хотим изменить. Так, в данном случае переменная sam получает для свойства Age значение из tom, а свойство Name изменяется.

Эта возможность может быть особенно актуальна, если в record, которую мы хотим скопировать, множество свойств, из которых мы хотим поменять одно-два.

Если надо скопировать значения всех свойств, то можно оставить пустые фигурные скобки:

`var person1 = new Person("Tom", 37);`
`var person2 = person1 with { };`

Как и обычные классы record-классы могут наследоваться.

Позиционные records

Records могут принимать данные для свойств через конструктор, и в этом случае мы можем сократить их определение. Например, пусть у нас есть следующая record Person:

`public record Person`
`{`
    `public string Name { get; init; }`
    `public int Age { get; init; }`
    `public Person(string name, int age)`
    `{`
        `Name = name; Age = age;`
    `}`
    `public void Deconstruct(out string name, out int age) => (name, age) = (Name, Age);`
`}`

Кроме конструктора здесь реализован деконструктор, который позволяет разложить объект Person на кортеж значений. И мы могли бы применить ее, например, следующим образом:

`var person = new Person ("Tom", 37);`
`Console.WriteLine(person.Name); // Tom`
 
`var (personName, personAge) = person;`
 
`Console.WriteLine(personAge);     // 37`
`Console.WriteLine(personName);    // Tom`

Выше определенную record Person можно сократить до позиционной record:

`public record Person(string Name, int Age);`

Это все определение типа. То есть мы говорим, что для типа Person будет создаваться конструктор, который принимает два параметра и присваивает их значения соответственно свойствам Name и Age, и что также автоматически будет создаваться деконструктор.