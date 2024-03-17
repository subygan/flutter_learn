---
emoji: 💻
title: Dart by example
---

## Main

`main()` is the entrypoint for application

```dart
main() {
    print('Hello, World');
}
```
Also, this works

```dart
main() => print('Hello')
```

## Values

```dart
main(){
    print( "1+1=${1+1}" ) //prints "1+1=2"
}
```

## For

```dart
main(){
    for (var i = 0; i<3; i++) {
        print( i )
    }
    
    var collection = [3,4,5]
    for (var x in collection) { //<<-- This works like python
        print(x)
    }
}
```

## conditionals

```dart
main(){
    if (7%2 == 0) {
        print('7 is even');
    ) else {
        print('7 is odd')
    }
    
    //ternary operators
    var isAlive = true;
    var monday = isAlive?'doctor': null;
    print(`$moday`) //prints "doctor"
}
````

## Null aware Operators

```dart
main(){
    var moday = 'doctor';
    var tuesday;
    var next = tuesday ?? monday; //Assign monday if tuesday is null
    
    var wednesday;
    next ??= wednesday; // Assign if not null
    
    String thursday;
    var length = thursday?.length; //Call function if not null
}
````

## Switch

```dart
main(){
var piece = 'knight';

switch(piece) {
    case 'queen':
    case 'bishop':
        print('diagonal');
    case 'knight':
        print('L-shape')
} 

}
````

```dart
class FoodSpoiledError extends StateError {
    FoodSpoiledError (String msg) : super(msg);
}

class Potato {
    int age;
    Potato(this.age);
    
    String peel() {
        if (age>4) {
            throw new FoodSpoiledError('Potato is spoiled')
        }
        return "peeled"
    }
}
main(){

    var p = Potato(7);
    
    try {
        p.peel();
    } on FoodSpoiledError catch(_) {
        print("no");
    }
    
    
    try {
        throw("potato"); //Anything can be thrown as an error;
    catch(_) {
        print("caught potato");
    }
    
    
    // Exceptions without try catch halt execution
    p.peel();
}
```


## Queue

```dart
main(){
    var q = new Queue.from([300, 200, 100, 500]); //Optimised for adding items to the head or tail.
    
    //Queues implement Iterable
    print(q.takewhile(i) => i > 100)); //prints "{300, 200}"
    
    //Consuming a queue
    while (q.first > 100) {
        q.removeFirst();
    }
    print(q); //print "{100,500}"
}
```

## Functions

```dart
yell(str) => str.toUpperCase(); //Valid function definition

List lines(String str) {
//^^ Return type
    return str.split('\n');
}

main(){
    var poemLines = lines(poem);
    print(yell(poemLines.first)); //POEM
    
    //Functions are first-class citizens
    var whisper = (String str) => str.toLowerCase();
    print(poemLines.map(whisper).last; //poem

}
poem = 'poem'
```

## Optional parameters

```dart
String yell(String str, [bool exclaim = false]) {
//                      ^^^^^^^^^^^ ordered optional parameter 
    var result = str.toLowerCase();
    if (exclaim) result = result + '!!!';
    return result
}

String whisper (String str, {bool mysteriously:false}) {
//                          ^^^^^^^ named optional parameter
    var result = str.toLowerCase();
    if (mysteriously) result = result + '....';
    return result;
}

main() {
    print (yell('Hello, World')); // prints "Hello, World"
    print (yell('Hello, World', true)); // prints "Hello, World!!!"
    print (whisper('Hello, World', mysteriously: true));
    }
```

## Lexical Scope

```dart
//variables declared inside loops will have a new version each time.
main(){
    var functions = [];
    
    for (var i=0; i<3; i++) {
        functions.add(() => i);
    }
    
    functions.forEach((fn) => print(fn())); // prints 0\n1\n2\n
}
```

## typedef

```dart
typedef bool Validator(int n); //Definition of a function to be used

main(){
    Validator validate = (int n) => n>10
    print('${both(5)}')
}
```

## unused variables

- use underscore to silence dartanalyzer

## Constants

```dart
import `dart:math`;

const name = "greg"; //Compile time variable

const Rectangle bounds = const Rectangle (0,0,5,5); //Even objects can be declared compile time
```

## Final

Final is used when the value is not known at compile time.
The values are immutable

```dart
main(){
    final foo = "hello";
    
    try {
        foo = 'goodbye'; //Assignment not possible
    } catch (e) {
        print('error')
    }
    
    var pos = new Position(4);
    
    try {
        pos.x = 100 //Not possible as the variables are declared as final
    } catch (e) {
        print('error')
}

class Position {

    final int x;
    final int y;
    Position(this.x) : y = 0;
}

```

## Static

Values are available in the class description itself instead of in an instance of a class

```dart

class Position {

    static int get maxX => 100; 
    
    static int maxY = 200;
}
main(){
    print(Position.maxX); //prints "100"
    print(Position.maxY); //prints "200"

}
```

## Classes

```dart
import 'dart:math';

class Position {

    // Properties, AKA class variables
    int x;
    int y;
    
    //Simple constructor
    Position(this.x, this.y);
    // ^^^^^ note that, constructor has the same name as the class
    
    //Additional constructors
    // object can be created like, var x = new Position.atOrigin 
    Position.atorigin(){
        x = 0;
        y = 0;
    }
    
    //Factory constructors
    factory Position.fromMap(Map m) => new Position(m['x'],m['y'])
    
    //methods
    double distanceTo(Position other) {
        var dx = other.x - x;
        var dy = other.y - y;
        
        return sqrt(dx*dx + dy*dy)
    }

}

main(){
    var origin = new Position();
    ..x = 0
    ..y = 0; //<<-- updating properties

    var p = new Position()
    ..x = -5
    ..y = 6;
    
    print(origin.distanceTo(p)); //7.8

}
```

## Initializer Lists + getters and setters

```dart

class Position {
    final int x;
    final int y;
    final double rad;
    
    //Initializer list allows fields to be defined 
    //before the constructor body.
    //This is required for final fields.
    Position(int x, int y)
        : this.x = x,
        this.y = y,
        rad = atan2(y, x);
        
    //Getter
    double get rad => rad
    //     ^^^ used to return value
    
    //Setter
    void set x(int val) {
    //   ^^^ used to return value
        _x = val;
    }
}

main(){
    var p = new Position(2,3); //Position object gets created
}
```

## Inheritance

```dart
//Abstract classes cannot be instantiated
// It can contain some implementation though
abstract class Animal {
    String name;
    Animal(this.name);
    String get noise;
}

class Dog extends Animal {
//        ^^^^^^ used to exten the animal class with new 

    Dog(String name): super(name);
    String get noise => 'bark!';
}

class Pikachu implements Animal {
//            ^^^^^ used to implement the Animal class
    String name = Pikachu;
    String get noise => 'pika!';
}

```

## Mixins

```dart
import `dart:math`;

class Position {
    int x;
    int y;
    
    double distanceTo(Position other) {
    
        var dx = other.x - x;
        var dy = other.y - y;
        return sqrt(dx*dx + dy*dy);
    }
}

class Square {

    int width;
    int height;
    
    int get area => width*height;
}



main(){

}
```

