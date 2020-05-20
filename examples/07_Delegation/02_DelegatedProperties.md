# Delegated Properties

Kotlin提供了[Delegated Properties](http://kotlinlang.org/docs/reference/delegated-properties.html)的机制，该机制允许将对set和get方法的调用委托给某个对象。  
在这种情况下，委托对象应具有方法`getValue`。对于可变属性，您还需要`setValue`。

```run-kotlin
import kotlin.reflect.KProperty

class Example {
    var p: String by Delegate()                                               // 1

    override fun toString() = "Example Class"
}

class Delegate() {
    operator fun getValue(thisRef: Any?, prop: KProperty<*>): String {        // 2     
        return "$thisRef, thank you for delegating '${prop.name}' to me!"
    }

    operator fun setValue(thisRef: Any?, prop: KProperty<*>, value: String) { // 2
        println("$value has been assigned to ${prop.name} in $thisRef")
    }
}

fun main() {
    val e = Example()
    println(e.p)
    e.p = "NEW"
}
```

1. 将类型为`String`的属性`p`委托给类`Delegate`的实例。委托对象是在`by`关键字之后定义的。
2. 委托方法。这些方法的签名始终如示例中所示。实现可能包含您需要的任何步骤。对于不可变属性，仅需要`getValue`。

### Standard Delegates 

Kotlin标准库包含一堆有用的委托，例如`lazy`，`observable`和其他。您可以按原样使用它们。
例如，`lazy`用于延迟初始化。

```run-kotlin
class LazySample {
    init {
      println("created!")            // 1
    }
    
    val lazyStr: String by lazy {
        println("computed!")          // 2
        "my lazy"
    }
}

fun main() {
    val sample = LazySample()         // 1
    println("lazyStr = ${sample.lazyStr}")  // 2
    println(" = ${sample.lazyStr}")  // 3
}
```

 1. 属性`lazy`在对象创建时未初始化。
 2. The first call to `get()` executes the lambda expression passed to `lazy()` as an argument and saves the result.
 3. Further calls to `get()` return the saved result.

默认情况下，惰性属性的求值是同步的：仅在一个线程中计算该值，并且所有线程将看到相同的值。如果不需要同步初始化委托，以便多个线程可以同时执行它，请将LazyThreadSafetyMode.PUBLICATION作为参数传递给lazy()函数。  
而且，如果您确定初始化将始终与使用该属性的线程在同一线程上进行，则可以使用LazyThreadSafetyMode.NONE：它不会产生任何线程安全保证和相关的开销。

### Storing Properties in a Map

属性委派可用于在map中存储属性。这对于诸如解析JSON或执行其他"dynamic"工作之类的任务非常方便。

```run-kotlin
class User(val map: Map<String, Any?>) {
    val name: String by map                // 1
    val age: Int     by map                // 1
}

fun main() {
    val user = User(mapOf(
            "name" to "John Doe",
            "age"  to 25
    ))

    println("name = ${user.name}, age = ${user.age}")
}
```

1. Delegates take values from the `map` by the string keys - names of properties.

您也可以将`mutable properties`委派给map。在这种情况下，map将根据属性分配进行修改。注意，您将需要`MutableMap`而不是只读的`Map`。