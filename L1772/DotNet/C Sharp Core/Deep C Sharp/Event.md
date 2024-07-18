#DeepCSharp 
[[Deep C Sharp]]

События сигнализируют системе о том, что произошло определенное действие. И если нам надо отследить эти действия, то как раз мы можем применять события.

В данном случае вначале определяется делегат AccountHandler, который принимает один параметр типа string. Затем с помощью ключевого слова event определяется событие с именем Notify, которое представляет делегат AccountHandler. Название для события может быть произвольным, но в любом случае оно должно представлять некоторый делегат.

//-----------------------------------------------------------------------------------------------

`internal class GayAccount`
`{`
    `public delegate void AccountHandler(string message);`
    `public event AccountHandler? Notify;`

	private decimal _balance;

	public decimal Balance
	{
		get { return _balance; }
		private set { _balance = value; }
	}

    public GayAccount(decimal deposit)
    {
        Balance = deposit;
    }

    public void Deposit(decimal amount)
    {
        Balance += amount;
        Notify?.Invoke($"Гей положил на счёт {amount}$ денег. Баланс: {Balance}$.");
    }

    public void Withdraw(decimal amount)
    {
        if (Balance > amount)
        {
            Balance -= amount;
            Notify?.Invoke($"Гей снял {amount}$ денег. Баланс: {Balance}$.");
        }
        else
        {
            Notify?.Invoke($"Недучная попытка снятия {amount}$, у гея не хватает денег. :( Баланс: {Balance}$");
        }
            
    }
`}`

//-----------------------------------------------------------------------------------------------

`using ConsoleApp1;`

`GayAccount Darkholm = new(300);`

`//Darkholm.Notify += new GayAccount.AccountHandler(DisplayMessage);`

`//Darkholm.Notify += delegate (string mes)`
`//{`
`//    Console.WriteLine(mes);`
`//};`

`Darkholm.Notify += DisplayMessage;`

`Darkholm.Deposit(150);`
`Darkholm.Withdraw(400);`
`Darkholm.Deposit(300);`
`Darkholm.Withdraw(50);`

`Darkholm.Notify -= DisplayMessage;`

`Darkholm.Withdraw(1000);`

`void DisplayMessage(string message)`
`{`
    `Console.ForegroundColor = ConsoleColor.Blue;`
    `Console.WriteLine(message);`
    `Console.ResetColor();`
`}`

//-----------------------------------------------------------------------------------------------

#так_можно_но_нихуя_не_нужно

    internal class GayAccount
    {
        public delegate void AccountHandler(string message);
        AccountHandler? notify;

        public event AccountHandler Notify
        {
            add
            {
                notify += value;
                Console.WriteLine("Обработчик добавлен");
            }
            remove
            {
                notify -= value;
                Console.WriteLine("Обработчик удалён");
            }
        }
        
    ![[Pasted image 20240712182556.png]]


