# Generics

[泛型](https://kotlinlang.org/docs/reference/generics.html)是一种泛型机制，它已经成为现代语言的标准。泛型类和函数通过封装独立于特定泛型类型的通用逻辑来提高代码的可重用性，比如`List<T>`中的逻辑独立于`T`。

### Generic Classes

The first way to use generics in Kotlin is creating generic classes.

```run-kotlin
//sampleStart
class MutableStack<E>(vararg items: E) {              // 1

  private val elements = items.toMutableList()

  fun push(element: E) = elements.add(element)        // 2

  fun peek(): E = elements.last()                     // 3

  fun pop(): E = elements.removeAt(elements.size - 1)

  fun isEmpty() = elements.isEmpty()

  fun size() = elements.size

  override fun toString() = "MutableStack(${elements.joinToString()})"
}
//sampleEnd

fun main() {
  val stack = MutableStack(0.62, 3.14, 2.7)
  stack.push(9.87)
  println(stack)

  println("peek(): ${stack.peek()}")
  println(stack)

  for (i in 1..stack.size()) {
    println("pop(): ${stack.pop()}")
    println(stack)
  }
}

```


1. 定义一个泛型类`MutableStack<E>`，其中`E`称为泛型类型参数。 在使用时，通过声明一个`MutableStack<Int>`，它被分配给一个特定的类型，例如`Int`。
2. 在泛型类内部，`E`可以像其他类型一样用作参数。
3. 还可以使用`E`作为返回类型。

Note that the implementation makes heavy use of Kotlin's shorthand syntax for functions that can be defined in a single expression.


### Generic Functions

你还可以使用 [泛型函数](https://kotlinlang.org/docs/reference/generics.html#generic-functions) 如果函数的逻辑独立于特定类型,例如，你可以编写一个实用函数来创建可变堆栈


```run-kotlin
class MutableStack<E>(vararg items: E) {              // 1

  private val elements = items.toMutableList()

  fun push(element: E) = elements.add(element)        // 2

  fun peek(): E = elements.last()                     // 3

  fun pop(): E = elements.removeAt(elements.size - 1)

  fun isEmpty() = elements.isEmpty()

  fun size() = elements.size

  override fun toString() = "MutableStack(${elements.joinToString()})"
}

//sampleStart
fun <E> mutableStackOf(vararg elements: E) = MutableStack(*elements)

fun main() {
  val stack = mutableStackOf(0.62, 3.14, 2.7)
  println(stack)
}
//sampleEnd
```

注意，编译器可以从`mutableStackOf`的参数推断出泛型类型，这样您就不必编写`mutableStackOf<Double>(…)`。
