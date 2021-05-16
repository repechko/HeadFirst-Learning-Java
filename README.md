# HeadFirst-Learning-Java

## TODO
### ~~Проверить, работает ли наследование от наследника непубличного класса классом из другого пакета.~~
- Получается наследоваться от наследного публичного класса и применять его методы. Но если приватный родительский класс находится в другом пакете, методы, к которым мы хотим обращаться должны быть публичными, если мы обращаемся к методу из класса, принадлежащего другому пакету.

### Посмотреть про статические методы инициализации объекта.

| Название главы | Страницы | Тезисы |
| :---: | :---: | :---: |
| ~~Использование библиотеки Java~~ | 149 - 188 (40 страниц) | Java позволяет использовать встроенные библиотеки (Java API) для ускорения написания кода. |
| ~~Прекрасная жизнь в Объектвилле~~ | 189 - 220 (32 страницы) | Наследование и полиморфизм |
| ~~Серьезный полиморфизм~~ | 221 - 258 (38 страниц) | Интерфейсы и абстрактные классы |
| ~~Жизнь и смерть объектов~~ | 259 - 295 (37 страниц) | Конструкторы и сборщик мусора |
| ~~Числа имеют значение~~ | 296 - 337 (42 страницы) | Числа и статические члены класса |
| Опасное поведение | 338 - 376 (39 страниц) | Обработка исключений |

---

### Глава № 6. Использование библиотеки Java
Между Array и ArrayList есть отличия. Массив обладает специфическим синтаксисом с квадратными скобками и предоставляет всего одну переменную экземпляра - length, которая возвращает длину массива. В то время как ArrayList является более гибким - обладает способностью динамически изменять размер, предоставляет множество методов для взаимодействия с элементами.

Arraylist объявляется с указанием типа в угловых скобках: 
```Java
ArrayList <String> = new ArrayList();
```

Так как списочные массивы являются массивами объектов, то для простых типов такие массивы объявляются через классы обертки:
```Java
ArrayList <Integer> = new ArrayList();
```
Java предоставляет широкий спектр библиотек, которые представлены классами внутри стандартных пакетов. Эти библиотеки позволяют пользоваться множеством функций, написанных авторами языка Java. ArrayList является одним из классов, поставляемых в этих библиотеках. Чтобы иметь возможность пользоваться такими классами, их нужно импортировать в начале класса:
```Java
import java.util.ArrayList
```
или, если хотим импортировать в свой код весь пакет util:
```Java
import java.util.*
```
Данный код позволяет нам обращаться к классу ArrayList просто по имени. Если же не делать импорт, то в коде при каждом обращении к списочному массиву мы должны писать `java.util.ArrayList`.

Разобраться в библиотеках нам поможет чтение документации. В качестве лучшего примера можно привести сайт [Oracle](https://docs.oracle.com/javase/7/docs/api/).

### Глава № 7. Наследование и полиморфизм
Наследование - механизм ООП, согласно которому существует некий абстрактный класс-родитель, содержащий в себе методы и переменные эксземпляра и передающий эти характеристики и поведение своим потомкам, которые в свою очередь могут переопределять сущетсвующие методы, а также создавать новые переменные и методы.

Уровни доступа по убыванию от самого строгого:
- private
- default
- protected
- public

Публичные (public) члены класса ***наследуются***, закрытые (private) - ***не наследуются***.

Переменные экземпляра не могут быть переопределены в дочернем классе, но их можно заново объявить.

Наследовать класс нельзя в трех случаях:
- класс не является публичным (нет ключевого слова public), при этом перед классом нельзя писать слово private. В данном случае наследование работает только внутри пакета, классы за его пределами не могут наследовать и даже пользоваться методами непубличного класса.
- класс объявлен как final, тогда он является конечной точкой в иерархии наследования. Если мы хотим защитить от переопределения метод, мы так же можем пометить его модификатором final.
- если у класса все конструкторы приватные

Также при наследовании мы можем задавать ссылку родительского типа и присваивать ей объект дочернего, что дает нам определенную степень гибкости. Например, мы можем написать метод, принимающий в качестве аргумента переменную типа родителя, и впоследствии обращаясь к данному методу, передавать ему ссылки на объекты дочернего типа.

При переопределении аргументы должны совпадать, а типы возвращаемых значений должны быть совместимы с типами оригинального метода родительского класса. Иначе это уже будет перегрузка, а не переопределение.

Уровень доступа переопределенного метода должен быть таким же или менее строгим. Так, переопределяя публичный метод в дочернем классе, мы не можем сделать его приватным.

Перегрузка - это наличие нескольких методов с одним именем, но разными наборами аргументов. При перегрузке уже можно изменять тип возвращаемого значения, а также выставлять более строгие уровни доступа. Но изменяя тип возвращаемого значения, обязательно нужно менять набор аргументов, иначе компилятор воспримет это как попытку переопределения, а при переопределении нельзя менять типа возвращаемого значения.

### Глава № 8. Интерфейсы и абстрактные классы
Абстрактный класс - класс, для которого нельзя создать экземпляр, компилятор не позволит. ***При этом мы можем использовать абстрактный тип в качестве ссылочного.*** Для объявления абстрактного класса достаточно указать ключевое слово abstract перед объявлением класса:
``` Java
abstract class Canine extends Animal {
/*длинный сложный код*/
}
```
Абстрактными могут быть не только классы, но и методы. Если абстрактный класс должен быть *расширен*, то абстрактный метод должен быть *переопределен*. Абстрактные методы не имеют тела. Их объявление выглядит так:
``` Java
public abstract void eat();
```

**Почему мы создаем абстрактные методы?**

Мы определяем некий метод, который обязательно должен присутствовать в каждом потомке. Это позволяет нам без опаски задавать в качестве аргументов методов, типов возвращаемых значений и массивов объект, имеющий ссылку типа родительского класса, потому что мы знаем, что поведение объектов типов дочерних классов, переопределяющих родительский абстрактный метод, будет схожим. Таким образом, если создать метод в неком классе, который принимает ссылку типа Animal, то наш код будет гораздо более компактным, чем если бы мы создавали отдельные методы для подтипов Animal - Dog, Cat, Wolf и тд.

Любой класс, который явно не расширяет другой класс, неявно унаследован от класса Object. В классе Object есть методы, которые
- позволяют сравнить два объекта - `obj1.equals(obj2)`, вернет значение типа boolean, метод рекомендуется переопределять в своем классе
- выведут класс объекта в формате "class Cat" - `obj1.getClass()`, вернет значение типа Class, метод финализирован, поэтому переопределить его нельзя (и не стоит)
- представят хэш-код для объекта - `obj1.hashCode()`, вернет значение типа int, метод рекомендуется переопределять в своем классе
- выведут сообщение с именем класса и цифрами, обычно этот метод переопределяется в каждом классе, чтобы выводить корректную информацию об объекте данного типа - `obj1.toString()`, вернет значение типа String

#### Опасность типа Object
Если мы напишем вот такой код
```Java
ArrayList<Object> myDogArrayList = new ArrayList<Object>();
Dog aDog = new Dog();
myDogArrayList.add(aDog);
```
он выполнится корректно, но если мы попробуем извлечь элемент из myDogArrayList и присвоить его объекту типа Dog
```Java
Dog d = myDogArrayList.get(0);
```
компилятор выдаст ошибку, потому что независимо от назначения объекта или ссылочного типа в тот момент, когда мы добавляли его в список, любой объект, выходящий из ArrayList<Object>, будет иметь тип Object.

![image](https://user-images.githubusercontent.com/67872457/115746572-7c94f400-a3a5-11eb-95d4-e9778575953e.png)

**Компилятор решает, сможем ли мы вызвать метод, основываясь на типе ссылки, а не на фактическом типе объекта. То есть метод, который вы вызываете, должен храниться в классе ссылки данного типа, и неважно, что представляет собой объект.** Как последствие этого: если вы обращаетесь к методу по ссылке родительского типа к присвоенному ей объекту дочернего типа, то при условии, что метод родительского класса переопределяется в дочернем, будет вызвана версия из дочернего класса. При этом вы не можете обратиться к методу дочернего класса, которого нет в родительском, потому что объявленная ссылка имеет тип **родительского** класса.

Наследники вниз по иерархии могут добавлять свои методы, и в итоге с объектами типов наследников мы можем выполнять действия, описанные как в методах родителей, так и в методах самих этих классов. При этом родители понятия не имеют о методах потомков.

Если мы хотим работать с извлеченным из списка типа Object элементом, который раньше относился к типу Dog, и работать с ним уже как с объектом типа Dog, то мы можем воспользоваться приведением типов. Такой код является допустимым и будет принят компилятором:
```Java
ArrayList<Object> myDogArrayList = new ArrayList<Object>();
Dog aDog = new Dog();
myDogArrayList.add(aDog);
Object o = myDogArrayList.get(0);
Dog d = (Dog) o;
```

Но стоит производить явное приведение типов, если только мы уверены, что объект действительно относится к приводимому типу. В случае если будет выполнено приведение к типу, которому объект не принадлежит, возникнет ошибка ClassCastException. Чтобы обезопасить себя, можно добавить условие перед приведением типа, которое будет проверять принадлежность объекта указанному классу:
```Java
if (o instanceof Dog) {
  Dog d = (Dog) o;
}
```

В Java невозможно множественное наследование для избежания "Смертоносноного Ромба Смерти" (СРС), когда в двух родителях присутствуют одинаковые методы и могут возникать конфликты, когда мы пытаемся обратиться к этим методам и Java не знает, чей метод запускать. **Поэтому родитель у класса всегда один.**

Во избежание СРС можно использовать интерфейс. Интерфейс в Java практически на 100% представляет собой чистый абстрактный класс. В интерфейсе все методы абстрактные.

Для определения интерфейса используем ключевое слово interface вместо class:
```Java
public interface Pet {...}
```

Для реализации интерфейса используем слово implements перед именем интерфейса:
```Java
public class Dog extends Canine implements Pet {...}
```

Также можно реализовывать сразу несколько интерфейсов, просто перечисляя их через запятую:
```Java
public class Dog extends Canine implements Pet, Saveable, Paintable {...}
```

Все методы интерфейса неявно считаются публичными и абстрактными, поэтому писать слова public и abstract необязательно и даже не говорит о "хорошем стиле" программирования.
```Java
public interface Pet {
  void beFriendly(); //у абстрактных методов нет тела
  //или
  public abstract void play();
}
```

Первый конкретный класс должен реализовывать все абстрактные методы, заданные в родительских классах или/и реализуемом интерфейсе.

Как узнать, когда нужно создавать класс, подкласс, абстрактный класс или интерфейс:
- Создавайте класс, который ничего не наследует (не считая Object), когда ваш новый класс не проходит проверку на соответствие другим типам.
- Создавайте дочерний класс, только когда вам нужно сделать **более специфичную** версию родительского класса и заменить или добавить новое поведение.
- Используйте абстрактный класс, когда хотите определить **шаблон** для группы подклассов и у вас есть хоть какой-нибудь код реализации, который смогут применять все подклассы. Делайте класс абстрактным, когда хотите получить гарантию того, что никто не сможет создать объекты данного типа.
- Пользуйтесь интерфейсом, когда хотите определить **роль**, которую смогут играть другие классы, невзирая на то, где они находятся в иерархии наследования.

Если мы хотим не целиком переопределить метод родительского класса, а лишь добавить некий код к уже имеющемуся, мы можем использовать ключевое слово `super`. Так, если в родительском классе Report есть метод `runReport() {...}`, то в дочернем, переопределяя данный метод, мы можем обратиться к родителю:
``` Java
public class BuzzwordReport extends Report {
  void runReport(){
    super.runReport(); //обращение к родительской версии метода
    ... //новый код
  }
}
```

### Глава № 9. Конструкторы и сборщик мусора

При работе с Java программистов интересуют две области памяти: в одной находятся объекты (куча), а в другой хранятся вызовы методов и локальные переменные (стек).

**Переменные экземпляра**  - переменные, которые объявляются внутри класса, но не внутри метода. Это поля, которые содержатся в каждом конкретном объекте типа этого класса и могут иметь разные значения для каждого из таких объектов.

**Локальные переменные** - переменные, которые объявляются внутри метода или являются его параметрами (аргументами). Существуют, пока метод находится в стеке (иными словами, пока метод не достиг закрывающей скобки).

Методы размещаются в стеке. Метод, выполняющийся в данный момент, всегда находится на вершине стека. Стек состоит из стековых фреймов, хранящих метод, а также локальные переменные.

Все объекты находятся в куче, даже объекты, на которые смотрят ссылки в виде локальных переменных. То есть если локальная переменная ссылается на объект, то в стек помещается только она. Сам же объект находится в куче, управляемой сборщиком мусора.

Переменные экземпляра размещаются в куче, внутри объекта, которому они принадлежат. При создании объекта, например, new CellPhone() Java сразу выделяет место в памяти (куче) для этого объекта. Для понимания количества требуемой памяти Java складывает объемы памяти, необходимые для переменных экземпляра. Так, если объект содержит переменную int, будет выделено 32 бита, если long - 64 бита. Если CellPhone содержит объект Antenna, то есть переменную, ссылающуюся на объект, Java выделяет место в куче, необходимое для хранения ссылки (**и только ссылки!**). Но так происходит до тех пор, пока мы не присвоим ссылке объект. Так при написании `private Antenna ant;` будет выделено место только для ссылки, тогда как при написании `private Antenna ant = new Antenna();` в куче сразу будет выделено место для объекта.

Конструктор - это код, который запускается при создании экземпляра класса. Вызывается посредством ключевого слова **new** перед именем класса. Конструктор в своем объявлении похож на метод с тем отличием, что у конструктора не указывается тип возвращаемого значения и его имя обязательно совпадает с именем класса. У любого класса есть конструктор по умолчанию (не принимающий никаких аргументов), даже если вы его явно не задаете. Однако, если создать в классе хотя бы один конструктор самостоятельно, компилятор уже не будет создавать пустой конструктор по умолчанию самостоятельно. Рекомендуется всегда создавать конструктор без аргументов и предусматривать в нем значения по умолчанию, чтобы облегчить программистам работу по созданию объектов. Создание конструктора выглядит так:
```Java
public CellPhone() {
  ...//код, выполняемый конструктором при создании нового объекта класса
}
```

Конструктор можно использовать для инициализации состояния объекта, то есть задания значений переменных:
```Java
public class Duck {
  int size;
  public Duck (int newSize) {
    size = newSize;
  }
}
```

Если вы не задали в конструкторе значения для переменных экземпляра, по умолчанию они устанавливаются для 0/0.0/false, а для ссылок - null.

Конструкторы можно перегружать, если задавать для них разные параметры и их типы. Таким образом, код ниже допустим:
```Java
public class Mushroom {
  public Mushroom (int size) {} //если мы знаем только размер
  public Mushroom () {} //если мы не знаем ничего
  public Mushroom (boolean isMagic) {} //если мы знаем, что гриб волшебный
  /*Ниже два варианта конструктора, когда мы знаем и о волшебных свойствах гриба, и о его размере. 
  Такой код допустим: хоть и параметры методов одинаковы, но они размещены в разном порядке*/
  public Mushroom (boolean isMagic, int size) {}
  public Mushroom (int size, boolean isMagic) {}
}
```

При создании объектов дочернего класса создаются переменные экземпляра всех родительских классов. Также при запуске дочернего конструтора запускаются конструкторы всех родительских классов, так как дочерние элементы зависят от родительских и это значит, что родительский объект должен быть полностью сформирован, включая все его переменные экземпляра, для корректной работы потомка. Таким образом, родительский конструктор должен быть завершен раньше, чем дочерний. Этот процесс называется связыванием (формированием цепочки) конструкторов. Наглядно это видно на картинке ниже:
![image](https://user-images.githubusercontent.com/67872457/116459791-4ceb5d80-a877-11eb-8444-f61ae4ff0062.png)

Если вы хотите напрямую вызвать родительский конструктор из дочернего, то внесите в дочерний конструктор вызов `super()`. Так будет вызван родительский конструктор по умолчанию. Комиплятор помещает неявно вызовы родительского конструктора посредством ключевого слова `super()`, если вы явно не указали этого.

Внутрь вызова `super()` мы можем передавать аргументы конструкторов родителя и тогда будут вызываться соответствующие конструкторы. Например, если у родителя есть конструктор `Animal(int size)`, в конструкторе потомка мы можем использовать вызов `super(10)`.

Для вызова одного конструктора из другого (в рамках одного класса) можно написать ключевое слово `this()`. Оно должно идти самым первым в конструкторе. Таким образом, мы не можем написать в одном конструкторе и `this()`, и `super()`:
``` Java
class Mini extends Car {
  Color color;
  
  public Mini() {
    this(Color.Red);
  }
  
  public Mini(Color c) {
    super("Mini");
    color = c;
    //Дальнейшая инициализация
  }
  
  /*код ниже не будет работать, так как в одном конструкторе и super(), и this(), а они оба должны идти в первом выражении
  public Mini(int size) {
    this(Color.Red);
    super(size);
  }*/
}
```

Область видимости локальных переменных ограничена рамками метода - пока метод не достиг закрывающей скобки, локальная переменная существует, но является видимой, только когда данный метод находится на вершине стека. Таким образом, если метод вызывает внутри себя другой метод, локальная переменная исходного метода не будет доступна во время выполнения вложенного.

Объект же живет, пока есть хотя бы одна ссылка на него. Когда же все ссылки на объект стерты, он становится доступен сборщику мусора. Три способа избавиться от ссылки на объект:
- ссылка перестает быть видимой, когда она существует в рамках метода
```Java
void go() {
  Life z = new Life();
}
```
- ссылке присваивается другой объект
```Java
Life z = new Life();
z = new Life();
```
- ссылке явно присваивается null
```Java
Life z = new Life();
z = null;
```

### Глава № 10. Числа и статические члены класса

Если поведение метода не зависит от значения переменной экземпляра, как, например, происходит с методом round() класса Math, то такой метод можно объявить статическим. Чтобы вызвать статический метод, мы должны обращаться не к переменной экземпляра, а к самому классу Math:
```Java
int x = Math.round(42.2);
int y = Math.min(56, 12);
int z = Math.abs(-343);
```

Таким образом, ключевое слово `static` позволяет работать методу без переменной экземпляра, так как его поведение не зависит от значения данной переменной.

Например, в коде ниже метод `play()` зависит от значения переменной экземпляра, так как внутри этого метода происходит обращение к переменной `title` и для каждой переменной экземпляра Song метод `play()` будет проигрывать разные композиции в зависимости от значения `title`:
```Java
public class Song {
  String title;
  public Song(String t) {
    title = t;
  }
  public void play() {
    SoundPlayer player = new SoundPlayer();
    player.playSound(title);
  }
}
```

Статические методы не могут использовать не статические переменные (то есть относящиеся к конкретному объекту) и не статические методы (так как статические методы не видят состояние полей). Так, например, код ниже не скомпилируется, так как метод `getSize()` и переменная `size` в методе `main` не привязаны ни к какому объекту:
```Java
public class Duck {
  private int size;
  
  public static void main (String[] args) {
    System.out.println("Размер равен" + size);
    System.out.println("Размер равен" + getSize());
  }
  
  public void setSize(int s) {
    size = s;
  }
  
  public void getSize() {
    return size;
  }
}
```

**Статическая переменная** - переменная, имеющая один экземпляр на весь класс. Так что если мы создаем несколько объектов типа Duck, представленного ниже, переменная `duckCount`, считающая количество уток, всё же будет одна:
```Java
public class Duck {
  private int size;
  private static int duckCount = 0;
  
  public Duck() {
    duckCount++;
  }
  
  public void setSize(int s) {
    size = s;
  }
  
  public void getSize() {
    return size;
  }
}
```

Если бы переменная `duckCount` не являлась статической, при каждом создании экземпляра класса Duck переменная `duckCount` определялась по новой для этого объекта возвращалась в значение 0. Слово static выручает нас в этом случае. Можно сказать, что статическая переменная живет в классе, а не в объекте.
![image](https://user-images.githubusercontent.com/67872457/117583831-754a4600-b11a-11eb-9aac-69fb7130e74b.png)

Статические переменные инициализируются при загрузке класса.

Чтобы объявить константу, надо указать идентификаторы static final. Так, например, число Пи в классе Math объявлено так:
```Java
public static final double PI = 3.141592653589793;
```

По соглашению об именовании **имена констант должны быть написаны в верхнем регистре с символами подчеркивания разделяющими слова!** Например, PI, FOO_X и т.д.

Инициализируются константы:
- при объявлении:
public static final int FOO_X = 25;
- в статическом блоке инициализации (этот код запускается сразу после загрузки класса перед вызовом любого статического метода и прежде, чем может быть использована любая статическая переменная):
```Java
static {
  FOO_X = 25;
}
```

Если статическую переменную не инициализировать, ей будет присвоено значение по умолчанию. Если же не инициализировать статическую финализированную переменную, то компилятор выдаст ошибку **variable FOO_X might not have been initialized**.

Присваивать значение финализированной переменной нужно либо во время её объявления, либо при создании конструктора.

Модификатор final можно использовать для обозначения не статических переменных, включая переменные экземпляра, локальные переменны и параметры методов - тогда значение этих переменных не будет меняться, а также чтобы запретить переопределение методов или создание дочерних классов.

Статический метод не имеет доступа к не статическим переменным и методам, но не статический метод может работать со статическими переменными и методами.

Если класс содержит исключительно статические методы и мы не хотим создавать его экземпляры, то можно сделать его конструктор приватным.

Методы Double.parseDouble(String), Integer.parseInt(String) принимают строковое написание числа и конвертируют его в соответствующий числовой тип. Например, `Integer.parseInt("2")` вернет целочисленное значение 2. Отличается получение из строки значения типа boolean: `boolean b = new Boolean("true").booleanValue();`.

Чтобы, наоборот, преобразовать любое значение в строку, стоит выполнить операцию `"" + foo`. Или можно воспользоваться методом toString из классов-оберток, принимающих соответствующий классу примитив. Например, код
```Java
int a = 1;
String b = Integer.toString(a);
```
запишет в b значение "1".

#### Форматирование чисел
Метод `String.format()` принимает два аргумента:
1. спецификаторы форматирования (начинается со знака %)
2. число, которое надо отформатирования

Параметры спецификатора форматирования (части в скобках необязательны, порядок следования параметров строгий):

%[номер аргумента][флаги][ширина][.разрядность]тип

![image](https://user-images.githubusercontent.com/67872457/118035574-6fec3600-b37c-11eb-92ec-d18cd2c77567.png)

В примере выше не указан номер аргумента, но все остальные спецификаторы присутствуют. Тип всегда обязателен и указывается последним.

Типы модификаторов: %d - целые числа (byte, short, int, char и их обертки, но не long), %f - дробные числа (float, double, их обертки и BigDecimal), %x - шестнадцатеричное число (byte, short, int, long, их обертки и BigInteger) - преобразует числа в их шестнадцатеричный эквивалент, %c - символ (byte, short, char, int и их обертки). Существует еще множество типов, но пока достаточно этих двух.

Например, строка ниже выведет число 1,000,000,000.46:
```Java
System.out.println(String.format(US, "%,.2f", 1000000000.455726));
```
Разберем эту строку по порядку:
- "US" означает американский стиль форматирования чисел (разделение разрядов запятыми)
- флаг "," означает разделение по разрядам, без этого идентификатора даже при наличии локализатора "US" число будет выведено без разделителей, а если убрать "US", но оставить флаг ",", то число будет выведено в виде 1 000 000 000.46
- .2 говорит компилятору, что нужно вывести два десятичных знака
- f означает тип дробного числа

#### Форматирование дат
Типы модификаторов:
- %tc выведет полный формат даты
- %tr - просто время
- %tA - день недели
- $tB - месяц
- %td - число

Пример:
```Java
Date today = new Date();
String.format("%tA %tB %td", today, today, today);
```
Возвратится, например, "Воскресенье, Ноябрь 28". Чтобы не писать переменную `today` три раза, можно модифицировать строку следующим образом:
```Java
String.format("%tA %<tB %<td", today);
```

Угловая скобка (<) - ещё один флаг, который говорит "используй предыдущий аргумент ещё раз".

**Для текущих временных меток применяется класс java.util.Date, для всего остального java.util.Calendar.** Но Calendar - абстрактный класс, поэтому мы будем работать с его потомками. Тип календаря, который мы получим, зависит от региональных настроек, и в большинстве стран это будет java.util.GrigorianCalendar. Но всегда можно найти библиотеки для работы с другими календарями, такими как японский, исламский, буддистский.

Чтобы получить экземпляр дочернего класса мы должны выполнить следующую команду:
```Java
Calendar cal = Calendar.getInstance();
```

В большей части стран мы получим в ответ экземпляр класса java.util.GrigorianCalendar.

Методы для редактирования даты:
![image](https://user-images.githubusercontent.com/67872457/118103901-7ebe0180-b3eb-11eb-9cb3-55fb6414110a.png)

Основные методы класса Calendar:
- **add(int field, int amount)** - добавляет или вычитает время из поля календаря
- **get(int field)** - возвращает значение заданного поля календаря
- **getInstance()** - возвращает экземпляр Calendar, можно задать региональные настройки
- **getTimeInMillis()** - возвращает время в миллисекундах (тип long)
- **roll(int field, boolean up** -  добавляет или вычитает время без изменения старших полей
- **set(int field, int value)** - устанавливает значения для заданного поля
- **set(int year, int month, int day, int hour, int minute)** - популярная разновидность метода set для детальной установки времени
- **setTimeInMillis(long millis)** - устанавливает время для объекта Calendar, основываясь на миллисекундах (тип long)

#### Статический импорт
Позволяет импортировать статические методы, переменные или перечисления, чтобы не набирать их по многу раз. Пример:
```Java
import static java.lang.System.out;
import static java.lang.Math.*;

public class TestBox {  
  out.println("Красивая квадратная коробка с ребром " + sqrt(4.0) + " метра.");
}
```
В примере выше благодаря статическому импорту мы легко можем обращаться к переменной `out` класса `System` и методу `sqrt` класса `Math`.

**Примечание:**
- во избежание путаницы и для улучшения читаемости кода лучше не злоупотреблять статическим импортом и прибегать к нему, если определенные статические члены используются часто
- существенная проблема статического импорта заключается в возможных конфликтах. Так, например, если у нас есть два класса с методом add(), то компилятор не сможет понять, какой из них использовать

### Глава № 11. Обработка исключений

Исключения - особые сущности, которые объявляются в методах для обработки непредвиденных ситуаций, таких как отключение сервера или отсутствие файла, к которому происходит обращение. Все исключения наследуются от класса Exception, который в свою очередь наследуется от Throwable. Throwable содержит методы `getMessage()` и `printStackTrace()`, который позволяет получить трассировку стека.

Чтобы выбросить исключения, нужен следующий код:
```Java
public void takeRisk() throws BadException /*так метод сообщает, что выбрасывает BadException*/ {
  if (abandonAllHope) {
    throw new BadException(); //создаем новый объект Exception и выбрасываем его
  }
  System.out.println("Конец опасного метода");
}
```

В случае выбрасывания исключения строчка "Конец опасного метода" выведена не будет, потому что код метода, выбрасывающего исключения, срабатывает только до момента выброса исключения. Если же исключение выброшено не будет, строка "Конец опасного метода" будет выведена при вызове метода.

Чтобы отловить, вот такой:
```Java
public void crossFingers() {
  try {
    anObject.takeRisk();
  } catch (BadException ex) {
    System.out.println("Аах!");
    ex.printStackTrace(); //если мы не справляемся с исключением, то хотя бы можем вывести трассировку стека
  }
}
```

Компилятор не даст нам оставить метод `crossFingers()` без отлавливания исключение, так как он знает, что метод `takeRisk()` объявил (выбрасывает) это исключение. Компилятор проверяет все исключения, кроме наследников RuntimeException. Мы можем выбрасывать, отлавливать и проверять и наследников RuntimeException, но это необязательно. Все исключения, которые интересны компилятору, называются проверяемыми.

Если требуется выполнить какой-то код независимо от того, будет выброшено исключение или нет, можно продублировать код в try и catch (**это плохо**) или использовать блок finally (**это good practice**):
```Java
try {
    turnOvenOn();
    x.bake();
} catch (BakingException ex) {
  ex.printStackTrace();
} finally {
  turnOvenOff();
}
```

- В итоге если один из методов блока try завершится неудачей, другие методы выполнятся не будут, и управление программным потоком немедленно перейдет в блок catch. После блока catch будет выполнен код из блока finally.
- Если блок try будет выполнен без выброса исключений, код в блоке catch выполняться не будет, а управление перейдет в блок finally.
- Если блоки try или catch содержат оператор return, то блок finally все равно будет выполнен. Поток перейдет к finally, а потом вернется к return.

Также метод может выбросить сразу несколько исключений (правда если два или более исключения, выбрасываемых методом, принадлежат одному родительскому классу, при объявлении можно ограничиться одним родительским классом):
```Java
public class Laundry () {
  public void doLaundry() throws PantsException, LingerieException {
    // Код, который может выбросить оба исключения
  }
}
```

Чтобы их обработать, нужно сделать несколько блоков catch:
``` Java
public class Foo {
  public void go() {
    Laundry laundry = new Laundry();
    try {
      laundry.doLaundry();
    } catch(PantsException pex) {
      // Восстановительный код
    } catch(LingerieException lex) {
      // Восстановительный код
    }
  }
}
```
