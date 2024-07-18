#ObjectOrientedProgramming 
[[Inheritance]]

Кроме обычных классов в C# есть абстрактные классы. Зачем они нужны? Классы обычно представляют некий план определенного рода объектов или сущностей. Например, мы можем определить класс Car для преставления машин или класс Person для представления людей, вложив в эти классы соответствующие свойства, поля, методы, которые будут описывать данные объекты. Однако некоторые сущности, которые мы хотим выразить с помощью языка программирования, могут не иметь конкретного воплощения. Например, в реальности не существует геометрической фигуры как таковой. Есть круг, прямоугольник, квадрат, но просто фигуры нет. Однако же и круг, и прямоугольник имеют что-то общее и являются фигурами. И для описания подобных сущностей, которые не имеют конкретного воплощения, предназначены абстрактные классы.

Абстрактный класс похож на обычный класс. Он также может иметь переменные, методы, конструкторы, свойства. Единственное, что при определении абстрактных классов используется ключевое слово abstract.

Но главное отличие абстрактных классов от обычных состоит в том, что мы НЕ можем использовать конструктор абстрактного класса для создания экземпляра класса.

Абстрактный класс от интерфейса в C# отличаются следующим образом:

- **Содержание**: **абстрактный класс может содержать реализованные методы**, в то время как **интерфейс только содержит сигнатуры методов**. 
- **Наследование**: **класс может наследовать только один абстрактный класс**, а **класс может реализовывать несколько интерфейсов**. 
- **Конструкторы**: **абстрактные классы могут иметь конструкторы**, в то время как **интерфейсы не могут**.
- **Поля и свойства**: **абстрактные классы могут иметь поля и свойства**, в то время как **интерфейсы могут иметь только свойства**. 
- **Цель использования**: **абстрактные классы обычно используются для создания базового класса, от которого наследуются другие классы**, в то время как **интерфейсы используются для определения контракта, который должны реализовать классы**. 
