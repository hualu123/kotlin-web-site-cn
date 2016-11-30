---
type: doc
layout: reference
category: "Syntax"
title: "异常"
---

# 异常

## 异常类

Kotlin中所有异常类都是 `Throwable` 的子类。
每一个异常都含有一条信息、栈回溯信息和一个可选的原因。

可以使用 *throw*{: .keyword }-expression 来抛出一个异常。

``` kotlin
throw MyException("Hi There!")
```

使用 `*try*{: .keyword }-expression` 来捕获一个异常。

``` kotlin
try {
    // some code
}
catch (e: SomeException) {
    // handler
}
finally {
    // optional finally block
}
```

可以有零或多个 *catch*{: .keyword } 块。*finally*{: .keyword } 块可以省略。
*catch*{: .keyword } 和 *finally*{: .keyword } 块应该至少出现一个。

### Try是一个表达式

*try*{: .keyword } 是一个表达式，比如，它可以有一个返回值。

``` kotlin
val a: Int? = try { parseInt(input) } catch (e: NumberFormatException) { null }
```

*try*{: .keyword }-expression 的返回值是 *try*{: .keyword } 中
最后一个表达式或者是 *catch*{: .keyword } 块中最后一个表达式。
*finally*{: .keyword } 块中的内容不会影响到表达式的结果。

## 受检的异常

Kotlin中没有受检的异常。这是有很多原因的，但是我们会提供一个简单的示例。

以下示例是JDK中`StringBuilder`类实现中的

``` java
Appendable append(CharSequence csq) throws IOException;
```

What does this signature say? It says that every time I append a string to something (a `StringBuilder`, some kind of a log, a console, etc.)
I have to catch those `IOExceptions`. Why? Because it might be performing IO (`Writer` also implements `Appendable`)...
So it results into this kind of code all over the place:

``` kotlin
try {
    log.append(message)
}
catch (IOException e) {
    // Must be safe
}
```

这样做是没有好处的，参阅 [Effective Java](http://www.oracle.com/technetwork/java/effectivejava-136174.html),Item 65: *不要忽略异常*。

Bruce Eckel在[Does Java need Checked Exceptions?](http://www.mindview.net/Etc/Discussions/CheckedExceptions) 中指出:

> 通过一些小程序测试得出的结论是规范的异常会提高开发者的生产效率和提高代码质量，但是大型软件项目的经验告诉我们一个不同的结论 - 这会降低生产效率并且不会对代码质量有明显提高。

相关引用：

* [Java's checked exceptions were a mistake](http://radio-weblogs.com/0122027/stories/2003/04/01/JavasCheckedExceptionsWereAMistake.html) (Rod Waldhoff)
* [The Trouble with Checked Exceptions](http://www.artima.com/intv/handcuffs.html) (Anders Hejlsberg)

## Java 互操作性

请在 [Java Interoperability section](java-interop.html) 异常章节中参阅Java交互相关信息。
