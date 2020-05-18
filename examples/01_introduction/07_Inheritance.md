# Inheritance

Kotlin完全支持传统的面向对象的继承机制。

```run-kotlin
open class Dog {                // 1
    open fun sayHello() {       // 2
        println("wow wow!")
    }
}

class Yorkshire : Dog() {       // 3
    override fun sayHello() {   // 4
        println("wif wif!")
    }
}

fun main() {
    val dog: Dog = Yorkshire()
    dog.sayHello()
}
```

1. Kotlin类在默认情况下是_final_。如果您希望允许类继承，请使用`open`修饰符标记该类。
2. Kotlin方法在默认情况下也是_final_。与类一样，`open`修饰符允许覆盖它们。
3. 当您在类名后面指定:`SuperclassName()`时，该类继承一个超类。空括号`()`表示超类默认构造函数的调用。
4. 重写方法或属性需要`override`修饰符。

### Inheritance with Parameterized Constructor

```run-kotlin
//sampleStart
open class Tiger(val origin: String) {
    fun sayHello() {
        println("A tiger from $origin says: grrhhh!")
    }
}

class SiberianTiger : Tiger("Siberia")                  // 1

fun main() {
    val tiger: Tiger = SiberianTiger()
    tiger.sayHello()
}
//sampleEnd
```


1. If you want to use a parameterized constructor of the superclass when creating a subclass, provide the constructor arguments in the subclass declaration.


### Passing Constructor Arguments to Superclass

```run-kotlin
//sampleStart
open class Lion(val name: String, val origin: String) {
    fun sayHello() {
        println("$name, the lion from $origin says: graoh!")
    }
}

class Asiatic(name: String) : Lion(name = name, origin = "India") // 1

fun main() {
    val lion: Lion = Asiatic("Rufo")                              // 2
    lion.sayHello()
}
//sampleEnd
```

1. 特别注意`name`既不是`var`也不是`val`,它是一个构造函数参数，其值被传递给超类`Lion`的`name`属性。
2. Creates an `Asiatic` instance with the name `Rufo`. The call invokes the `Lion` constructor with arguments `Rufo` and `India`.

