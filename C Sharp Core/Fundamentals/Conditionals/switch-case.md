#fundamentals 
[[Conditionals]]

Оператор `switch` выбирает список операторов, который нужно выполнить, на основе соответствия шаблона выражению соответствия.

Person Aharon = new(1, "Aharon", 20, "Armenian");
Person Dima = new(2, "Dima Nedovodnenko", 25, "Russian");
Person Russel = new(3, "Jerusalem", 32, "Dagestani");
Person Alex = new(4, "Alex", 22, "Ukrainian");
Person GayBoy = new(5, "Fred", 78, "Minion");

switch (GayBoy.Nationality)
{
case "Armenian":
    Console.WriteLine("Pashol nahuy Aharon!");
    break;

case "Russian":
    Console.WriteLine("More whiskey?");
    break;
        
case "Dagestani":
    Console.WriteLine("No AK-47 please.");
    break;

case "Ukrainian":
    Console.WriteLine("Welcome to the club, gachimuchi legend!");
    break;

default: 
    Console.WriteLine("U r not in the list, go away please, u fucking Ciganian.");
    break;
}

Оператор `switch` выполняет _список операторов_ в первом _разделе switch_, _шаблон ветви_ которого соответствует выражению соответствия, а [условие ветви](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/statements/selection-statements#case-guards), если оно есть, равно `true`. Оператор `switch` оценивает шаблоны ветвей в порядке, в котором они указаны в коде, сверху вниз. Компилятор создает ошибку, если оператор `switch` содержит недостижимую ветвь. Это ветвь, которая уже была обработана в верхнем регистре или шаблон которой невозможно сопоставить.