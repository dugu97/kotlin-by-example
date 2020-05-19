# Object Keyword

Kotlin中的类和对象的工作方式与大多数面向对象的语言相同：*class*是一个蓝图, *object*是一个类的实例。通常，您定义一个类，然后创建该类的多个实例：
```run-kotlin
import java.util.Random

class LuckDispatcher {                    //1 
    fun getNumber() {                     //2 
        var objRandom = Random()
        println(objRandom.nextInt(90))
    }
}

fun main() {
    val d1 = LuckDispatcher()             //3
    val d2 = LuckDispatcher()
    
    d1.getNumber()                        //4 
    d2.getNumber()
}
```

1. Defines a blueprint.
2. Defines a method.
3. Creates instances.
4. Calls the method on instances. 

In Kotlin you also have the [**object** keyword](https://kotlinlang.org/docs/reference/object-declarations.html). It is used to obtain a *data type with a single implementation*.

如果您是Java用户，并且想了解“*single*”的含义，可以考虑**Singleton**模式：即使您有2个线程尝试创建该类，它也可以确保仅创建该类的一个实例。 。

要在Kotlin中实现此目标，您只需声明一个`object`：没有类，没有构造函数，只有一个`lazy instance`。Why lazy? 因为它将在访问对象时创建一次。否则，它甚至不会被创建。

### `object` Expression

这是 `object` **expression**的基本典型用法：简单的对象/属性结构。
在类声明中不需要这样做：创建一个对象，声明其成员并在一个函数中访问它。像这样的对象通常在Java中作为匿名类实例创建。

```run-kotlin
fun rentPrice(standardDays: Int, festivityDays: Int, specialDays: Int): Unit {  //1

    val dayRates = object {                                                     //2
        var standard: Int = 30 * standardDays
        var festivity: Int = 50 * festivityDays
        var special: Int = 100 * specialDays
    }

    val total = dayRates.standard + dayRates.festivity + dayRates.special       //3

    print("Total price: $$total")                                               //4

}

fun main() {
    rentPrice(10, 2, 1)                                                         //5
}
```

1. 创建带有参数的函数。
2. 创建一个在计算结果值时要使用的对象。
3. 访问对象的属性。
4. 打印结果。
5. 调用函数。这是实际创建对象的时间。

### `object` Declaration

您还可以使用`object` **declaration**。它不是表达式，不能在变量赋值中使用。您应该使用它直接访问其成员：

```run-kotlin
object DoAuth {                                                 //1 
    fun takeParams(username: String, password: String){         //2 
        println("input Auth parameters = $username:$password")
    }
}

fun main(){
    DoAuth.takeParams("foo", "qwerty")                          //3
}

```

1. Creates an object declaration.
2. Defines the object method.
3. Calls the method. This is when the object is actually created.

### Companion Objects

An object declaration inside a class defines another useful case: the **companion object**. 
Syntactically it's similar to the static methods in Java: you call object members using its *class name* as a qualifier.
If you plan to use a companion object in Kotlin, consider using a *package-level* function instead.  

类内的对象声明定义了另一种有用的情况：**companion object**。
从语法上讲，它类似于Java中的静态方法：您可以使用对象的*class name*作为限定符来调用对象成员。
如果您打算在Kotlin中使用伴随对象，请考虑改用*package-level*函数。

```run-kotlin
class BigBen {                                  //1 
    companion object Bonger {                   //2
        fun getBongs(nTimes: Int) {             //3
            for (i in 1 .. nTimes) {
                print("BONG ")
            }
        }
    }
}

fun main() {
    BigBen.getBongs(12)                         //4
}
```

1. Defines a class.
2. 定义一个`companion object`。其名称可以省略。
3. Defines a companion object method.
4. 通过类名称调用伴随对象方法。
