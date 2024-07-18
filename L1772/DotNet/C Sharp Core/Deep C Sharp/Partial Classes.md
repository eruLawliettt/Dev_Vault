#DeepCSharp 
[[Deep C Sharp]]

Классы могут быть частичными. То есть мы можем иметь несколько файлов с определением одного и того же класса, и при компиляции все эти определения будут скомпилированы в одно.

Например, определим в проекте два файла с кодом. Не столь важно как эти файлы будут называться. Например, PersonBase.cs и PersonAdditional.cs. В одном из этих файлов (без разницы в каком именно) определим следующий класс:

`public partial class Person`
`{`
    `public void Move()`
    `{`
        `Console.WriteLine("I am moving");`
    `}`
`}`
`А в другом файле определим следующий класс:`

`public partial class Person`
`{`
    `public void Eat()`
    `{`
        `Console.WriteLine("I am eating");`
    `}`
`}`

Таким образом, два файла в проекте содержит определение одного и того же класса Person, которые содержат два разных метода. И оба определенных здесь класса являются частичными. Для этого они определяются с ключевым словом partial.

`Robot GayBot = new(300, "F98");`

`GayBot.TurnOn();`
`GayBot.Shoot(300);`
`Console.WriteLine();`
`GayBot.Shoot(100000);`

`  internal partial class Robot`
`  {`
    `  public bool IsAlive { get; set; }`
    `  public bool IsRunning { get; set; }`

      public Robot(int ammo, string guntype)
      {
          IsAlive = true;
          IsRunning = false;
          Ammo = ammo;
          GunType = guntype;

      }

      public void TurnOn()
      {
          IsRunning = true;
          Console.WriteLine("GayBot Activated!!!");
      }

`  }`
` internal partial class Robot
` {``
    ` public int Ammo { get; set; }`
	 `public string GunType { get; set; }`

     public void Shoot(int bullets)
     {
         if (Ammo >= bullets)
         {
             for (int i = 0; i < bullets; i++)
             {
                 Console.WriteLine("TRATATATATA FUCK U FUCKING MAN TRATATATTA!");
                 Ammo -= bullets;
             }
         }
             
         else
             Console.WriteLine("BEEP BEEP MOTHERFUCKER! NO AMMO! GOING BACK!");
     }

` }`


### Частичные методы

Частичные классы могут содержать частичные методы. Такие методы также опреляются с ключевым словом partial. Причем определение частичного метода без тела метода находится в одном частичном классе, а реализация этого же метода - в другом частичном классе.

Стоит отметить, что по умолчанию к частичным методам применяется ряд ограничений:

- Они не могут иметь модификаторы доступа
    
- Они имеют тип void
    
- Они не могут иметь out-параметры
    
- Они не могут иметь модификаторы `virtual, override, sealed, new` или `extern`

`public partial void Scream();` 

 `public partial void Scream()`
 `{`
     `Console.WriteLine("AAAAAAAAAHHH!");`
 `}`