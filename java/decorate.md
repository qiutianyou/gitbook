# Java 修饰符
Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

* default (即缺省，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。

* private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）

* public : 对所有类可见。使用对象：类、接口、变量、方法

* protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。

以下表格说明了各修饰符的访问权限：

|修饰符|当前类|同一包内|子孙类|其他包|其他子孙包类|
|:-:   |:-:   |:-:   |:-:   |:-:   |:-:   |
|default   | Y  | Y  | N  | N  | N  |
|protected   | Y  | Y  | Y  |  N |Y/N <a href="#">请见详解</a>   |
|public   | Y  | Y  | Y  | Y  |  Y  |
|private   | Y  | N  | N  | N  | N  |

# Java protected 关键字详解

很多介绍Java语言的书籍(包括《Java编程思想》)都对protected介绍的比较的简单，基本都是一句话，就是: 被 protected 修饰的成员对于本包和其子类可见。这种说法有点太过含糊，常常会对大家造成误解。实际上，protected的可见性在于两点：

* 基类的 protected 成员是包内可见的，并且对子类可见；
* 若子类与基类不在同一包中，那么在子类中，子类实例可以访问其从基类继承而来的protected方法，而不能访问基类实例的protected方法。

<a href="http://www.runoob.com/w3cnote/java-protected-keyword-detailed-explanation.html">demo参考</a>
