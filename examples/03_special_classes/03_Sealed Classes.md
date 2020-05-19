# Sealed Classes

[Sealed classes](https://kotlinlang.org/docs/reference/sealed-classes.html) 让您限制继承的使用。声明密封的类后，只能从声明密封的类的同一文件内部对其进行子类化。不能在声明密封类的文件之外对它进行子类化。 

```run-kotlin
sealed class Mammal(val name: String)                                                   // 1

class Cat(val catName: String) : Mammal(catName)                                        // 2
class Human(val humanName: String, val job: String) : Mammal(humanName)

fun greetMammal(mammal: Mammal): String {
    when (mammal) {                                                                     // 3
        is Human -> return "Hello ${mammal.name}; You're working as a ${mammal.job}"    // 4
        is Cat -> return "Hello ${mammal.name}"                                         // 5     
    }                                                                                   // 6
}

fun main() {
    println(greetMammal(Cat("Snowy")))
}
```

1. Defines a sealed class. 
2. 定义子类。请注意，所有子类必须位于同一文件中。
3. Uses an instance of the sealed class as an argument in a `when` expression. 
4. 执行smartcast，将`Mammal`投向`Human`。
5. 执行smartcast，将`Mammal`投向`Cat`。
6. 这里没有其他情况，因为涵盖了密封类的所有可能的子类。对于非密封的超类，将需要`else`。


