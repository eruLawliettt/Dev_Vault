#ObjectOrientedProgramming 
[[Access Modifiers]]

Ключевое слово `public` является модификатором доступа для типов и членов типов. Общий доступ является уровнем доступа с максимальными правами. Ограничений доступа к общим членам не существует.

Пример
В следующем примере объявляются два класса: PointTest и Program. Доступ к открытым членам x и y класса PointTest осуществляется непосредственно из класса Program.

`class PointTest`
`{`
    `public int x;`
    `public int y;`
`}`

`class Program`
`{`
    `static void Main()`
    `{`
        `var p = new PointTest();`
        `// Direct access to public members.`
        `p.x = 10;`
        `p.y = 15;`
        `Console.WriteLine($"x = {p.x}, y = {p.y}");`
    `}`
`}`
`// Output: x = 10, y = 15`

Если уровень доступа public изменить на private или protected, будет выводится следующее сообщение об ошибке:

"PointTest.y" недоступен из-за его уровня защиты.