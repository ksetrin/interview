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
1. objects are memory structure in different memory positions for the set they should be completely different objects
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
1. In JavaScript, if you define a function as a variable, the variable name will be hoisted but you cannot access until JS execution encounters its definition.
    ```
    console.log(square(5)); //TypeError: square is not a function
     
    var square = function(n) { 
      return n * n; 
    }
    ```
    But
    ```
    console.log(square(5)); // return 25
    function square(n) { return n * n; }
    ```
1. Use .bind() when you want that function to later be called with a certain context, useful in events. Use .call() or .apply() when you want to invoke the function immediately, with modification of the context.
1. Разница между call и apply только в том, что apply принимает вторым параметром массив, а call принимает несколько аргументов
    ```
    theFunction.apply(valueForThis, arrayOfArgs)
    theFunction.call(valueForThis, arg1, arg2, ...)
    ```
1. .call exapmle
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
1. .apply
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
1. Bind attaches a brand new this to a given function. In bind’s case, the function is not executed instantly like Call or Apply.
1. JavaScript scope well (Closures as well)
    Global scope - 
    Local Scope/Function scope - 
    Block scope(Introduced in ES6) - 
    A closure is a function that returns another function and wraps data. 
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
    A closure is a function that returns another function and wraps data. The above string generator qualifies for a closure. 
    !!! Побольше про замыкания и генераторы
    If you defined one more function in the second level function, that can access all parent’s variables. - замыкание

1. this in object scope
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
1. Object.freeze allows us to freeze an object so that existing properties cannot be modified.
    ```
    var marks = {physics: 98, maths:95, chemistry: 91};
    finalizedMarks = Object.freeze(marks);
    finalizedMarks["physics"] = 86; // throws error in strict mode
    console.log(marks); // {physics: 98, maths: 95, chemistry: 91}
    ```
1. Object.seal is slightly different from the freeze. It allows configurable properties but won’t allow new property addition or deletion or properties.
    ```
    var marks = {physics: 98, maths:95, chemistry: 91};
    Object.seal(marks);
    delete marks.chemistry; // returns false as operation failed
    marks.physics = 95; // Works!
    marks.greek = 86; // Will not add a new property
    ```
1. These four things you should remember about prototypical inheritance.
    Class properties are bound using this
    Class methods are bound using prototype object
    To inherit properties, use call function passing this object
    To inherit methods, use Object.create to link prototypes of parent and child
    Always set child class constructor to itself for getting the right identity of its objects
    Note: These are things happens under the hood even with new class syntax.
1. Callbacks are the functions those executed after an I/O operation is done
1. Hoisting
    Hoisting is a process of pushing the declared variables to the top of the program while running it. For Ex:
    ```
    doSomething(foo); // used before
    var foo; // declared later
    ```
    https://developer.mozilla.org/en-US/docs/Glossary/Hoisting?source=post_page-----23a5c0fa4d0d----------------------
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
1. 
1. 
