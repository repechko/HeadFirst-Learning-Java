# HeadFirst-Learning-Java


| Название главы | Страницы | Время прочтения | Тезисы |
| :---: | :---: | :---: | :---: |
| ~~Использование библиотеки Java~~ | 149 - 188 (40 страниц) | многа... | Java позволяет использовать встроенные библиотеки (Java API) для ускорения написания кода. |
| ~~Прекрасная жизнь в Объектвилле~~ | 189 - 220 (32 страницы) | многа... | Наследование и полиморфизм. |
| Серьезный полиморфизм | 221 - 258 (38 страниц) | многа... | Интерфейсы и абстрактные классы. |

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

