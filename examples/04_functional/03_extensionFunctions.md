# Extension Functions and Properties

Kotlin允许您使用[扩展](https://kotlinlang.org/docs/reference/extensions.html)机制将新成员添加到任何类中。即，扩展有两种类型：扩展功能和扩展属性。它们看起来很像普通的函数和属性，但有一个重要的区别：您需要指定扩展的类型。

```run-kotlin
data class Item(val name: String, val price: Float)                                   // 1  

data class Order(val items: Collection<Item>)  

fun Order.maxPricedItemValue(): Float = this.items.maxBy { it.price }?.price ?: 0F    // 2  
fun Order.maxPricedItemName() = this.items.maxBy { it.price }?.name ?: "NO_PRODUCTS"

val Order.commaDelimitedItemNames: String                                             // 3
    get() = items.map { it.name }.joinToString()

fun main() {

    val order = Order(listOf(Item("Bread", 25.0F), Item("Wine", 29.0F), Item("Water", 12.0F)))
    
    println("Max priced item name: ${order.maxPricedItemName()}")                     // 4
    println("Max priced item value: ${order.maxPricedItemValue()}")
    println("Items: ${order.commaDelimitedItemNames}")                                // 5

}
```

1. 定义`Item`和`Order`的简单模型。 `Order`可以包含`Item`对象的集合。
2. Adds extension functions for the `Order` type.  
3. Adds an extension property for the `Order` type.
4. 直接在`Order`实例上调用扩展功能。
5. 访问`Order`实例的扩展属性。

甚至有可能在`null`引用上执行扩展。`在扩展功能中`，您可以检查对象是否为`null`并在代码中使用结果：
`?:`含义: `对象A` ?: `对象B` 表达式，意思为，当对象`A`值为`null`时，那么它就会返回后面的对象`B`。

```run-kotlin
//sampleStart
fun <T> T?.nullSafeToString() = this?.toString() ?: "NULL"  // 1
//sampleEnd
fun main() {
    println(null.nullSafeToString())
    println("Kotlin".nullSafeToString())
}
```
