# A Tour of the Dart Language
* [一个基础的Dart程序](#basic_dart)
* [重要的概念](#import_concepts)
* [关键字](#keyword)
* [变量](#variables)
  * [默认值](#default_value)
  * [Final and const](#final_const)
* [内置类型](#buildin_type)
  * [数字](#numbers)
  * [字符串](#strings)
  * [列表](#lists)

<h2 id="basic_dart">一个基础的Dart程序</h2>

以下的代码使用了许多Dart最基础的特性：
``` Dart
// Define a function.
printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
main() {
  var number = 42; // Declare and initialize a variable.
  printInteger(number); // Call a function.
}
```

以下是针对所有（或几乎所有）Dart apps都会使用到的东西：

<font color=#008f92>// This is a comment.</font><br/>
一个单行注释。Dart也支持多行注释和文档注释。

<font color=#008f92>int</font><br/>
表示类型。还有一些其他的内置类型，如String、List以及bool。

<font color=#008f92>42</font><br/>
数字文字。数字文字是一种编译时常数。

<font color=#008f92>print()</font><br/>
一个展示输出内容的便捷的方式。

<font color=#008f92>$variableName (or ${expression})</font><br/>
字符串插值：在字符串文本中包含变量或表达式的字符串等效项。

<font color=#008f92>main()</font><br/>
启动应用程序执行的特殊、必需的顶级函数。

<font color=#008f92>var</font><br/>
一种定义不指定类型的变量的方法。

<h2 id="import_concepts">重要的概念</h2>

在学习DART语言时，请记住以下事实和概念：

* 可以放在变量中的所有东西都是对象，每个对象都是类的实例。偶数、函数和NULL都是对象。所有对象都继承自Object类。
* 虽然Dart是强类型的，但类型注释是可选的，因为Dart可以推断类型。在上面的代码中，数字被推断为int类型。如果要显式声明不需要任何类型，请使用特殊类型Dynamic。
* Dart支持泛型类型，如List<int>(整数列表)或List<dynamic>(任何类型的对象列表)。
* Dart支持顶级函数(如main())以及绑定到类或对象的函数(分别为静态方法和实例方法)。您还可以在函数中创建函数(嵌套或本地函数)。
* 类似地，Dart支持顶级变量，以及绑定到类或对象(静态和实例变量)的变量。实例变量有时称为字段或属性。
* 与Java不同，Dart没有public、protected和private关键字。如果标识符以下划线(_)开头，则该标识符对其库是私有的。
* 标识符可以字母或下划线(_)开头，后跟这些字符加数字的任何组合。
* 需要清楚的界定好某条语句是一个表达式还是陈述式。
* Dart工具可以报告两种类型的问题：警告和错误。警告只是表明您的代码可能无法工作，但它们并不妨碍程序的执行。错误可以是编译时错误，也可以是运行时错误。编译时错误根本阻止代码执行；运行时错误会导致在代码执行时引发异常。

<h2 id="keyword">关键字</h2>

下表列出了DART语言专门处理的单词。<br/>
<img src="./keyword.jpg" alt="keyword" title="keyword" width="1000"/><br/>
上标1的单词是内置标识符。避免使用内置标识符作为标识符。如果您试图为类名或类型名使用内置标识符，则会发生编译时错误。

带有上标2的两个字是较新的、有限的保留字，它们与在DART 1.0版本之后添加的异步支持有关。您不能在任何用异步、异步*或同步*标记的函数体中使用async, await或 yield作为标识符。有关更多信息，请参见异步支持。

关键字表中的所有其他字都是保留字。不能使用保留字作为标识符。

<h2 id="variables">变量</h2>

下面是创建变量并对其进行初始化的示例:
``` Dart
var name = 'Bob';
```

变量存储引用。名为name的变量包含一个带有“Bob”值的字符串对象的引用。

name变量的类型推断为String，但您可以通过指定它来更改该类型。如果对象不限于单个类型，请按照设计准则指定对象或动态类型。
``` Dart
dynamic name = 'Bob';
```

另一种选择是显式声明可能推断的类型：
``` Dart
String name = 'Bob';
```

> Note:本页遵循《编码风格指南》，对局部变量使用var而不是类型注释。

<h2 id="default_value">默认值</h2>

未初始化变量的初始值为null。即使是数值类型的变量，初始值也是null，因为数字就像Dart中的其他东西一样,也是对象。
``` Dart
int lineCount;
assert(lineCount == null);
```

在生产代码中 ```assert()``` 的调用会被忽略。在开发过程中，除非条件为真，否则 ```assert(condition)``` 。有关详细信息，请参见断言。

<h2 id="final_const">Final and const</h2>

如果您不希望更改变量，请使用Final或const来取代var，或者除此之外额外再加上一个类型声明。一个final变量只能被赋值一次。常量变量是编译时常数.(常量变量是隐式的final变量。)一个final的顶级变量或类变量在第一次使用时被初始化。

>Note:实例变量可以是final，但不能是const。

下面是创建和设置一个final变量的示例：
``` Dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
```

你无法更改一个final变量的值：
``` Dart
name = 'Alice'; // Error: a final variable can only be set once.
```

对希望成为编译时常量的变量使用const。如果const变量是class级别，则将其标记为static const。在声明变量时，将值设置为编译时常量，如数字或字符串文字、常量变量或常量算术运算的结果：
``` Dart
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```

const关键字不仅仅用于声明常量变量。您还可以使用它来创建常量值，以及声明创建常量值的构造函数。任何变量都可以有一个常量值。
``` Dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalent to `const []`
```

您可以在const声明的初始化表达式中省略const，就像上面的Baz一样。有关详细信息，请参见不要重复使用const。您可以更改不是final、不是const的值，即使它之前有一个常量值：
``` Dart
foo = [1, 2, 3]; // Was const []
```

无法更改常量变量的值：
``` Dart
baz = [42]; // Error: Constant variables can't be assigned a value.
```

有关使用const创建常量值的详细信息，请参阅 Lists, Maps, 和 Classes。

<h2 id="buildin_type">内置类型</h2>

DART语言特别支持以下类型：

* numbers
* strings
* booleans
* lists (also known as arrays)
* maps
* runes (for expressing Unicode characters in a string)
* symbols

可以使用文本初始化这些特殊类型的任何对象。例如， ``` 'this is a string'``` 是一个字符串文本，而 ```true``` 是一个布尔文本。

因为Dart中的每个变量都指向一个对象—— 一个类的实例 —— 您通常可以使用构造函数来初始化变量。有些内置类型有自己的构造函数。例如，您可以使用 ```Map()``` 构造函数来创建映射。

<h2 id="numbers">数字</h2>
Dart Numbers 有两种:

```int```<br/>
整数值不大于64位，具体取决于平台。在Dart虚拟机上, 取值范围为 -2<sup>63</sup>~2<sup>63</sup>-1。使用JavaScript Numbers编译为JavaScript的DART，允许值为-2<sup>53</sup>~2<sup>53</sup>-1。

```double```<br/>
64位(双精度)浮点数，符合IEEE 754标准。

```int```和```double```都是```num```的子类型。num类型包括基本运算符，例如+、-、/和*，您还可以在其中找到```abs()```、```cill()```和```log()```等方法。(像 >> 这样的位运算符是在int类中定义的。)如果num及其子类型没有您要寻找的内容，则<a href="https://api.dartlang.org/stable/2.0.0/dart-math/dart-math-library.html">dart:math<a/>库可能会包含。

Integers是没有小数点的数字。下面是一些定义整数文本的示例：
``` Dart
int x = 1;
int hex = 0xDEADBEEF;
```

如果一个数字包含小数点，那么它就是double。下面是一些定义double文本的示例：
``` Dart
double y = 1.1;
double exponents = 1.42e5;
```

下面是如何将字符串转换为数字的方法，反之亦然：
``` Dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

int类型支持传统的位移(<<，>>)，与(&)和或(|)运算符。例如：
``` Dart
assert((3 << 1) == 6); // 0011 << 1 == 0110
assert((3 >> 1) == 1); // 0011 >> 1 == 0001
assert((3 | 4) == 7); // 0011 | 0100 == 0111
```

数字是编译时的常量。许多算术表达式也是编译时的常量。它们的运算结果也是可以计算到数字的编译时常量。
``` Dart
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
```

<h2 id="strings">字符串</h2>

DART字符串是UTF-16编码的单元序列。可以使用单引号或双引号创建字符串：
``` Dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

你可以通过使用```${expression}```将表达式的值嵌入字符串中。如果表达式是标识符，则可以省略{}。Dart可以调用对象的toString()方法获取与对象相对应的字符串。
``` Dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, ' +
        'which is very handy.');
assert('That deserves all caps. ' +
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. ' +
        'STRING INTERPOLATION is very handy!');
```

>Note:==操作符可以测试两个对象是否相等。如果两个字符串包含相同的代码单元序列，则它们是相等的。

你可以让字符串保持相邻或者使用+运算符来连接字符串：
``` Dart
ar s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
    'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

另一种创建多行字符串的方法：使用带有单引号或双引号的三元引号：
``` Dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

你可以通过添加前缀r创建一个"原始"的字符串:
``` Dart
var s = r'In a raw string, not even \n gets special treatment.'
```

如何在字符串中表示Unicode字符,请参考Runes获取详情。

字符串文本是编译时常量，只要任何插值表达式的值是null或数字、字符串或布尔值,它都是一个编译时常量。

``` Dart
// These work in a const string.
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// These do NOT work in a const string.
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
```

有关使用字符串的详细信息，请参阅字符串和正则表达式。

<h2 id="booleans">布尔</h2>

为了表示布尔值，DART有一个命名为bool的类型。只有两个对象具有bool类型：布尔文本true和false，它们都是编译时常量。

DART的类型安全性意味着您不能使用以下代码```if(nonbooleanValue)```或```assert (nonbooleanValue)```。相反，需要显式地检查值，如下所示：
```Dart
// Check for an empty string.
var fullName = '';
assert(fullName.isEmpty);

// Check for zero.
var hitPoints = 0;
assert(hitPoints <= 0);

// Check for null.
var unicorn;
assert(unicorn == null);

// Check for NaN.
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```

<h2 id="lists">列表</h2>

在几乎所有编程语言中，可能最常见的集合就是数组了，或者说是有序的对象组。在Dart中，数组是List对象，所以大多数人都叫它们列表。

Dart list文本与JavaScript数组文本。下面是一个简单的Dart list：
``` Dart
var list = [1, 2, 3];
```

>Note:分析器推断list具有类型List<int>。如果尝试向此列表添加非整数对象，分析器分析或程序运行时将引发错误。有关更多信息，请阅读类型推断。





