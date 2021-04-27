# HeadFirst-Learning-Java

## TODO
~~Проверить, работает ли наследование от наследника непубличного класса классом из другого пакета.~~
- Получается наследоваться от наследного публичного класса и применять его методы. Но если приватный родительский класс находится в другом пакете, методы, к которым мы хотим обращаться должны быть публичными, если мы обращаемся к методу из класса, принадлежащего другому пакету.

| Название главы | Страницы | Тезисы |
| :---: | :---: | :---: |
| ~~Использование библиотеки Java~~ | 149 - 188 (40 страниц) | Java позволяет использовать встроенные библиотеки (Java API) для ускорения написания кода. |
| ~~Прекрасная жизнь в Объектвилле~~ | 189 - 220 (32 страницы) | Наследование и полиморфизм |
| ~~Серьезный полиморфизм~~ | 221 - 258 (38 страниц) | Интерфейсы и абстрактные классы |
| Жизнь и смерть объектов | 259 - 295 (37 страниц) | Конструкторы и сборщик мусора |

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

### Глава № 7. Прекрасная жизнь в Объектвилле
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

### Глава № 8. Серьезный полиморфизм
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
компилятор выдаст ошибку, потому что независимо от назначения объекта или ссылочного типа в тот момент, когда мы добавляли его в список, любой объект выходящий из ArrayList<Object>, будет иметь типа Object.

![image](https://user-images.githubusercontent.com/67872457/115746572-7c94f400-a3a5-11eb-95d4-e9778575953e.png)

**Компилятор решает, сможем ли мы вызвать метод, основываясь на типе ссылки, а не на фактическом типе объекта. То есть метод, который вы вызываете, должен храниться в классе ссылки данного типа, и неважно, что представляет собой объект.** Как последствие этого: если вы обращаетесь к методу по ссылке родительского типа к присвоенному ей объекту дочернего типа, то при условии, что метод родительского класса переопределяется в дочернем, будет вызывана версия из дочернего класса. При этом вы не можете обратиться к методу дочернего класса, которого нет в родительском, потому что объявленная ссылка имеет тип **родительского** класса.

Наследники вниз по иерархии могут добавлять свои методы, и в итоге с объектами типов наследников мы можем выполнять действия, описанные как в методах родителей, так и в методах самих этих классов. При этом родители понятия не имеют о методах потомков.

Если мы хотим работать с извлеченной из списка типа Object элемент, который раньше относился к типу Dog, и работать с ним уже как с объектом типа Dog, то мы можем воспользоваться приведением типа. Такой код является допустимым и будет принят компилятором:
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

Все методы интерфейса неявно считаются публичными и абстрактными, поэтому писать слова public и abstract необязательно и даже не говорит о "хорошем стиле" программирования".
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

### Глава № 9. Жизнь и смерть объектов

При работе с Java программистов интересуют две области памяти: в одной находятся объекты (куча), а в другой хранятся вызовы методов и локальные переменные (стек).

**Переменные экземпляра**  - переменные, которые объявляются внутри класса, но не внутри метода. Это поля, которые содержатся в каждом конкретном объекте типа этого класса и могут иметь разные значения для каждого из таких объектов.

**Локальные переменные** - переменные, которые объявляются внутри метода или являются его параметрами (аргументами). Существуют, пока метод находится в стеке (иными словами, пока метод не достиг закрывающей скобки).

Методы размещаются в стеке. Метод, выполняющийся в данный момент, всегда находится на вершине стека. Стек состоит из стековых фреймов и хранит метод, а также локальные переменные.

Все объекты находятся в куче, даже объекты, на которые смотрят ссылки в виде локальных переменных. То есть если локальная переменная ссылается на объект, то в стек помещается только она. Сам же объект находится в куче, управляемой сборщиком мусора.

Переменные экземпляра размещаются в куче, внутри объекта, которому они принадлежат. При создании объекта, например, new CellPhone() Java сразу выделяет место в памяти (куче) для этого объекта. Для понимания количества требуемой памяти Java складывает количества памяти, необходимые для переменных экземпляра. Так, если объект содержит переменную int, будет выделено 32 бита, если long - 64 бита. Если CellPhone содержит объект Antenna, то есть переменную, ссылающуюся на объект, тогда Java выделяет место в куче, необходимое для хранения ссылки (**и только ссылки!**). Но так происходит до тех пор, пока мы не присвоим ссылке объект. Так при написании `private Antenna ant;` будет выделено место только для ссылки, тогда как при написании `private Antenna ant = new Antenna();` в куче сразу будет выделено место для объекта.

Конструктор - это код, который запускается при создании экземпляра класса. Вызывается посредством ключевого слова **new** перед именем класса. Конструктор в своем объявлении похож на метод с тем отличием, что у конструктора не указывается тип возвращаемого значения и его имя обязательно совпадает с именем класса. У любого класса есть конструктор по умолчанию, даже если вы его явно не задаете. Однако, если создать в классе хотя бы один конструктор самостоятельно, компилятор уже не будет создавать пустой конструктор по умолчанию самостоятельно. Создание конструктора выглядит так:
```Java
public CellPhone() {
  ...//код, выполняемый конструктором при создании нового объекта класса
}

Конструктор можно использовать для инициализации состояния объекта, то есть задания переменных:
```Java
public class Duck {
  int size;
  public Duck (int newSize) {
    size = newSize;
  }
}
```

Конструкторы можно перегружать, если задавать для них разные параметры и типы аргументов. Таким образом, код ниже допустим:
```Java
public class Mushroom {
  public Mushroom (int size) {} //если мы знаем только размер
  public Mushroom () {} //если мы не знаем ничего
  public Mushroom (boolean isMagic) {} //если мы знаем, что гриб волшебный
  //ниже два варианта конструктора, когда мы знаем и о волшебных свойствах гриба, и о его размере. 
  //Такой код допустим, хоть и параметры методов одинаковы, но они размещены в разном порядке
  public Mushroom (boolean isMagic, int size) {}
  public Mushroom (int size, boolean isMagic) {}
}
```

