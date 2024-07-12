#fundamentals 
[[Conditionals]]

Оператор `if` в C Sharp — простейшая конструкция, позволяющая сделать ветвление. Заданная в условии операция будет выполняться, если результатом вычислений и сравнений станет логическая истина (true).

int Dima = 23

if (Dima < 23) 
{ 
	Console.WriteLine("Not good."); 
} 
else if (Dima == 23)
{ 
	Console.WriteLine("Perfect!"); 
} 
else
{
	Console.WriteLine("Oh fuck! Too much!"); 
}

//-------------------------------------------------------------

object Dima = new(height=120, penis=23);

if(Dima.height == 120)
{
	if(Dima.penis >= 23)
		{
			cw("all good.")
		}
	else
		{
			cw("height good, penis small.")
		}
}
else
{
	cw("shit!")
}

//-------------------------------------------------------------

Request(code=200, flag="green");

if(Request.flag == "red") 
{ 
	Request.code = 404; 
}

