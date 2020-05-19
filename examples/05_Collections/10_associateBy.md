# associateBy, groupBy

函数`associateBy`和`groupBy`从指定键索引的集合元素中构建映射。键在`keySelector`参数中定义。
您还可以指定一个可选的`valueSelector`来定义将存储在map元素的`value`中的内容。

`associateBy`和`groupBy`之间的区别在于它们如何使用相同的键处理对象：
* `associateBy` 使用最后一个合适的元素作为值。
* `groupBy` 构建所有合适元素的列表并将其放入值中。

返回的`map`保留原始集合的输入迭代顺序。

```run-kotlin
fun main() {

//sampleStart

    data class Person(val name: String, val city: String, val phone: String) // 1

    val people = listOf(                                                     // 2
      Person("John", "Boston", "+1-888-123456"),
      Person("Sarah", "Munich", "+49-777-789123"),
      Person("Svyatoslav", "Saint-Petersburg", "+7-999-456789"),
      Person("Vasilisa", "Saint-Petersburg", "+7-999-123456"))
      
    val phoneBook = people.associateBy { it.phone }                          // 3
    val cityBook = people.associateBy(Person::phone, Person::city)           // 4
    val peopleCities = people.groupBy(Person::city, Person::name)            // 5

//sampleEnd

    println("People: $people")
    println("Phone book: $phoneBook")
    println("City book: $cityBook")
    println("People living in each city: $peopleCities")
  
//运行结果如下:
//People: [Person(name=John, city=Boston, phone=+1-888-123456), Person(name=Sarah, city=Munich, phone=+49-777-789123), Person(name=Svyatoslav, city=Saint-Petersburg, phone=+7-999-456789), Person(name=Vasilisa, city=Saint-Petersburg, phone=+7-999-123456)]
//Phone book: {+1-888-123456=Person(name=John, city=Boston, phone=+1-888-123456), +49-777-789123=Person(name=Sarah, city=Munich, phone=+49-777-789123), +7-999-456789=Person(name=Svyatoslav, city=Saint-Petersburg, phone=+7-999-456789), +7-999-123456=Person(name=Vasilisa, city=Saint-Petersburg, phone=+7-999-123456)}
//City book: {+1-888-123456=Boston, +49-777-789123=Munich, +7-999-456789=Saint-Petersburg, +7-999-123456=Saint-Petersburg}
//People living in each city: {Boston=[John], Munich=[Sarah], Saint-Petersburg=[Svyatoslav, Vasilisa]}
}
```

1. Defines a data class that describes a person.
2. Defines a collection of people.
3. 建立从电话号码到其所有者信息的map。这里的`it.phone`是`keySelector`。没有提供`valueSelector`，因此map的值本身就是`Person`对象。
4. 建立从电话号码到业主居住城市的map。这里的`Person :: city`是`valueSelector`，因此map的值仅包含城市。
5. 建立从城市到居住在那里的人的map。map的值是`人员姓名列表`。
