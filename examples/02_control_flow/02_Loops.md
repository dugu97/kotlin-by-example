# Loops

Kotlin支持所有常用的循环：`for`，`while`，`do-while`

### `for`

`for` in Kotlin works the same way as in most languages.

```run-kotlin
fun main(args: Array<String>) {
//sampleStart
    val cakes = listOf("carrot", "cheese", "chocolate")
    
    for (cake in cakes) {                               // 1
        println("Yummy, it's a $cake cake!")
    }

//sampleEnd
}
```

1. Loops through each cake in the list.

### `while` and `do-while`

`while` and `do-while` constructs work similarly to most languages as well.

```run-kotlin
fun eatACake() = println("Eat a Cake")
fun bakeACake() = println("Bake a Cake")

fun main(args: Array<String>) {
    var cakesEaten = 0
    var cakesBaked = 0
    
    while (cakesEaten < 5) {                    // 1
        eatACake()
        cakesEaten ++
    }
    
    do {                                        // 2
        bakeACake()
        cakesBaked++
    } while (cakesBaked < cakesEaten)

}
```

1. Executes the block while the condition is true.
2. Executes the block first and then checking the condition.

### Iterators(迭代器)

您可以通过在类中实现`iterator`运算符来定义自己的迭代器。

```run-kotlin
class Animal(val name: String)

class Zoo(val animals: List<Animal>) {

    operator fun iterator(): Iterator<Animal> {             // 1
        return animals.iterator()                           // 2
    }
}

fun main() {

    val zoo = Zoo(listOf(Animal("zebra"), Animal("lion")))

    for (animal in zoo) {                                   // 3
        println("Watch out, it's a ${animal.name}")
    }

}
```

1. 在类中定义迭代器。它必须命名为“ iterator”并具有“ operator”修饰符。
2. 返回迭代器要求需要实现以下的方法
  * `next()`: `Animal`
  * `hasNext()`: `Boolean`
3. Loops through animals in the zoo with the user-defined iterator.

迭代器可以以类型或扩展函数声明。
