# HeadFirst-Learning-Java


| Название главы | Страницы | Время прочтения | Тезисы |
| :---: | :---: | :---: | :---: |
| ~~Использование библиотеки Java~~ | 149 - 188 (40 страниц) | многа... | Java позволяет использовать встроенные библиотеки (Java API) для ускорения написания кода. |
| Прекрасная жизнь в Объектвилле | 189 - 220 (32 страницы) | многа... | Наследование и полиморфизм. |

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
