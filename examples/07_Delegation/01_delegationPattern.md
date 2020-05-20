# Delegation Pattern

Kotlin支持在本机级别轻松实现[委托模式](https://kotlinlang.org/docs/reference/delegation.html)，而无需任何样板代码。

```run-kotlin
interface SoundBehavior {                                                          // 1
    fun makeSound()
}

class ScreamBehavior(val n:String): SoundBehavior {                                // 2
    override fun makeSound() = println("${n.toUpperCase()} !!!")
}

class RockAndRollBehavior(val n:String): SoundBehavior {                           // 2
    override fun makeSound() = println("I'm The King of Rock 'N' Roll: $n")
}

// Tom Araya is the "singer" of Slayer
class TomAraya(n:String): SoundBehavior by ScreamBehavior(n)                       // 3

// You should know ;)
class ElvisPresley(n:String): SoundBehavior by RockAndRollBehavior(n)              // 3

fun main() {
    val tomAraya = TomAraya("Thrash Metal")
    tomAraya.makeSound()                                                           // 4
    val elvisPresley = ElvisPresley("Dancin' to the Jailhouse Rock.")
    elvisPresley.makeSound()
}
```


1.  Defines the interface `SoundBehavior` with one method. 
2.  The classes `ScreamBehavior` and `RockAndRollBehavior` implement the interface and contain their own implementations of the method.
3.  `TomAraya`和`ElvisPresley`类也实现了接口，但没有实现该方法。而是将方法调用委托给委托对象。委托对象是在`by`关键字之后定义的。如您所见，不需要样板代码。
4.  在类型为`TomAraya`的`tomAraya`或类型为`ElvisPresley`的`elvisPresley`上调用makeSound（）时，该调用将委派给相应的委托对象。
