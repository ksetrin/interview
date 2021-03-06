1. В JavaScript функции – это объекты.
1. Движок (встроенный, если это браузер) читает («парсит») текст скрипта. Затем он преобразует («компилирует») скрипт в машинный язык. После этого машинный код запускается и работает достаточно быстро.
1. Различные окна/вкладки не знают друг о друге. Иногда одно окно, используя JavaScript, открывает другое окно. Но даже в этом случае JavaScript с одной страницы не имеет доступа к другой, если они пришли с разных сайтов (с другого домена, протокола или порта).
Это называется «Политика одинакового источника» (Same Origin Policy). Чтобы обойти это ограничение, обе страницы должны согласиться с этим и содержать JavaScript-код, который специальным образом обменивается данными.
1. Если атрибут src установлен, содержимое тега script будет игнорироваться.
    ```
    <script src="file.js">
      alert(1); // содержимое игнорируется, так как есть атрибут src
    </script>
    ``` 
1. Почему нужны точка с запятой?
    ```
    [1, 2].forEach(alert) // works
    ```
    ```
    alert("Сейчас будет ошибка") // alert works
    [1, 2].forEach(alert) // Uncaught TypeError: Cannot read property '2' of undefined
    ```
    JavaScript не вставляет точку с запятой перед квадратными скобками [...]
    ```
    alert("Сейчас будет ошибка")[1, 2].forEach(alert)
    ```
1. Директива `use strict` переключает движок в «современный» режим, изменяя поведение некоторых встроенных функций. Позже в учебнике мы увидим подробности.
1. Типы данных
    1. number для любых чисел: целочисленных или чисел с плавающей точкой. (примитив)
    1. string для строк. Строка может содержать один или больше символов, нет отдельного символьного типа. (примитив)
    1. boolean для true/false. (примитив)
    1. null для неизвестных значений – отдельный тип, имеющий одно значение null. (примитив)
    1. undefined для неприсвоенных значений – отдельный тип, имеющий одно значение undefined. (примитив)
    1. object для более сложных структур данных.
    1. symbol для уникальных идентификаторов. (примитив) (добавлен в ES6)
1. Оператор "=" возвращает значение
    ```
    if (a = 1 + 2) { alert(a);}
    ```
    Вызов x = value записывает value в x и возвращает его.
1. Оператор запятая предоставляет нам возможность вычислять несколько выражений, разделяя их запятой (,). Каждое выражение выполняется, но возвращается результат только последнего.
    ```
    let a = (1 + 2, 3 + 4);
    alert( a ); // 7 (результат 3 + 4)
    ```
    ```// три операции в одной строке
    for (a = 1, b = 3, c = a * b; a < 10; a++) {
     ...
    }
    ```
1. Битовый сдвиг
    ```
    console.log(15 / 2) // 7.5
    console.log(math.floor(15 / 2)) // 7
    console.log(15 >> 1) // 7
    ```
    Выровнять картинку по центру экрана
    ```
    (screenWidth - imageWidth) >> 1
    ```
1. Значения null и undefined равны == друг другу и не равны любому другому. Значения null и undefinded равны друг другу при нестрогом сравнении.
1. И «&&» находит первое ложное значение
   Другими словами, И возвращает первое ложное значение. Или последнее, если ничего не найдено.
1. Разница в том, что И возвращает первое ложное значение, а ИЛИ –  первое истинное.
1. Если определить функцию как переменную, то эта переменная будет объявлена, но не будет доступна для вызова
    ```
    console.log(square); // undefined (переменная объявлена)
    console.log(square(5)); // TypeError: square is not a function (не доступна для вызова)
     
    var square = function(n) { 
      return n * n; 
    }
    ```
    Но
    ```
    console.log(square(5)); // return 25
    function square(n) { return n * n; }
    ```
1. Метод .bind() позволяет привязать контекст к функции, этот метод только привязывает контекст и не вызывает саму функцию.
    ```
    let user = {
        firstName: "Вася"
    };
    
    function func() {
        alert(this.firstName);
    }
    
    let funcUser = func.bind(user);
    funcUser(); // Вася
    ```
1. Методы .call() и .apply() позволяют вызвать функцию с определнным контекстом, но this передается в качестве аргумента   
1. Разница между call и apply только в том, что apply принимает вторым параметром массив, а call принимает несколько аргументов
    ```
    theFunction.apply(valueForThis, arrayOfArgs)
    theFunction.call(valueForThis, arg1, arg2, ...)
    ```
    Пример с .call()
    ```
    var mathLib = {
        pi: 3.14,
        area: function(r) {
            return this.pi * r * r;
        },
        circumference: function(r) {
            return 2 * this.pi * r;
        }
    };
    
    mathLib.area(2);
    12.56
    
    Now use constant pi with 5 decimals precision
    
    mathLib.area.call({pi: 3.14159}, 2);
    12.56636
    ```
    Пример с .apply()
    ```
    var cylinder = {
        pi: 3.14,
        volume: function(r, h) {
            return this.pi * r * r * h;
        }
    };
    cylinder.volume.call({pi: 3.14159}, 2, 6);
    75.39815999999999
    cylinder.volume.apply({pi: 3.14159}, [2, 6]);
    75.39815999999999
    ```
1. Существует несколько оружений (scope)
    1. Глобальное окружение (global scope) 
    1. Локальное окружение (local/function) 
    1. Блочное окружение (block) 
1.  Замыкание это функция (родитель), которая возвращает другую функцию (потомок) с доступом к переменным функции(родителя) 
    ```
    function generator(input) {
          var index = 0;
          return {
               next: function() {
                       if (index < input.length) {
                            index += 1;
                            return input[index - 1];
                       }
                       return "";
               } 
          }
    }
    var mygenerator = generator("boomerang");
    mygenerator.next(); // returns "b"
    mygenerator.next() // returns "o"
    ```
    Все вложенные функции (потомки) будут иметь доступ к переменным своих родителей
1. Внутри объекта в методах можно использовать this и он будет ссылаться на текущий объект
    ```
    var person = {
        name: "Stranger",
        age: 24,
        get identity() {
            return {who: this.name, howOld: this.age};
        }
    }
    person.identity; // returns {who: "Stranger", howOld: 24}
    ```
1. Object.freeze позволяет "заморозить" объект таким образом, что станет невозможно изменять его свойства 
    ```
    var marks = {physics: 98, maths: 95, chemistry: 91};
    finalizedMarks = Object.freeze(marks);
    finalizedMarks["physics"] = 86; // throws error in strict mode
    console.log(marks); // {physics: 98, maths: 95, chemistry: 91}
    ```
1. Object.seal немного отличается от freeze. Позволяет изменять свойства, но не позволяет добавлять или удалять свойства 
    ```
    var marks = {physics: 98, maths: 95, chemistry: 91};
    Object.seal(marks);
    delete marks.chemistry; // returns false as operation failed
    marks.physics = 95; // Works!
    marks.greek = 86; // Will not add a new property
    ```
1. Прототипное наследование
    Class properties are bound using this
    Class methods are bound using prototype object
    To inherit properties, use call function passing this object
    To inherit methods, use Object.create to link prototypes of parent and child
    Always set child class constructor to itself for getting the right identity of its objects
    Note: These are things happens under the hood even with new class syntax.
1. Колбэки (callbacks) это функции, которые выполняются, когда  I/O операция завершена
1. Поднятие (hoisting) - функции и переменные объявляются в самом начале программы
    ```
    doSomething(foo); // used before
    var foo; // declared later
    ```
    Переменная foo объявлена позже ее использования, но благодаря поднятию ошибки не происходит
    JavaScript "поднимает" только объявление, но не инициализацию.
1. a JavaScript VM does two things while running a program:
    First scan the program, collect all the variable and function declarations and assign memory spaces for it.
    Run the program now by filling variable values assigned any, if not, fill undefined
1. Event bubbling and capturing are two ways of event propagation in the HTML DOM API when an event occurs in an element inside another element, and both elements have registered a handler for that event. The event propagation mode determines in which order the elements receive the event.
    For Ex: Bubbling Model
    ```
    <div onClick="divHandler()">
        <ul onClick="ulHandler">
            <li id="foo"></li>
        </ul>
    </div>
    <script>
    function handler() {
     // do something here
    }
    function divHandler(){}
    function ulHandler(){}
    document.getElementById("foo").addEventListener("click", handler)
    </script>
    ```
1. Spread operator
    Под капотом оператор расширения использует итераторы, чтобы перебирать элементы. Так же, как это делает for..of.
1. Как можно переписать рекурсивную функцию? - Можно переписать с использованием стека (что более оптимально, так как стек может иметь большую вложенность)
1. interface vs abstract class javascript
interface is often some kind of type declaration, whereas class or abstract class are class declaration, which in JS are just constructors, though they often define a specific "type" of values. abstract are a special case in between the two because they define a new concrete value (a constructor in JS) but cannot be instantiated without being subclassed.

Bottom line, interfaces are declaration in the space of types, whereas [abstract] class are declaration in the space of values. In typescript for instance you can bridge the two using class implements. In JavaScript the term interface more often refers to the general shape of behaviour of a specific type of value returned by some API (see https://developer.mozilla.org/en-US/docs/Web/API/Event where the term interface is used to describe different kind of events).



Interfaces only describe what properties and methods should be implemented, and don’t describe how methods should work.

But abstract classes may describe how a method works, like in regular classes. For example:

abstract class MyClass {
   abstract method_1() // a method with no implementation

   method_2() { // a method with implementation
      // do something
   }
}
Interfaces look like:

interface MyInterface {
   method_1(): void;
   method_2(): string;
}
1. 
1. 
1. 
1. 
1. 
1. 
1. 
1. 
1. 
1. 
1. 
1. 
1. 
