注意: 这个指南假定你正在使用Babel

# 1.types

## 1.1基本类型:

你可以直接获取到基本类型的值：String,number,boolean, null, undefined,symbol

Symbols 不能被正确的polyfill。 所以在不能原生支持symbol类型的环境[浏览器]中，不应该使用 symbol 类型。

## 1.2复杂类型

复杂类型赋值是获取到他的引用的值。 相当于传引用object，

Array， function，References

# 2.赋值

## 2.1所有的赋值都用const，避免使用var. 首选const，避免修改const

Why? 因为这个确保你不会改变你的初始值，重复引用会导致bug和代码难以理解

## 2.2如果你一定要对参数重新赋值，那就用let，而不是var.

Why? 因为let是块级作用域，而var是函数级作用域

## 2.3注意： let、const都是块级作用域

# 3.Objects

## 3.1使用字面值创建对象.

## 3.2当创建一个带有动态属性名的对象时，用计算后属性名

Why? 这可以使你将定义的所有属性放在对象的一个地方.

## 3.3用对象方法简写.

## 3.4用属性值缩写, 这样写的更少且更可读

## 3.5将你的所有缩写放在对象声明的开始.

## 3.6只对那些无效的标示使用引号 ''.

Why? 通常我们认为这种方式主观上易读。他优化了代码高亮，并且页更容易被许多JS引擎压缩。

## 3.7不要直接调用Object.prototype上的方法，如hasOwnProperty, propertyIsEnumerable, isPrototypeOf。

Why? 在一些有问题的对象上， 这些方法可能会被屏蔽掉 - 如：{ hasOwnProperty: false } - 或这是一个空对象Object.create(null)

## 3.8对象浅拷贝时，更推荐使用扩展运算符[就是...运算符]，而不是Object.assign。获取对象指定的几个属性时，用对象的rest解构运算符[也是...运算符]更好。

# 4.Arrays

## 4.1 用字面量赋值。

## 4.2 用Array#push 代替直接向数组中添加一个值。

## 4.3 用扩展运算符做数组浅拷贝，类似上面的对象浅拷贝

## 4.4 用 ... 运算符而不是Array.from来将一个可迭代的对象转换成数组。

## 4.5 用 Array.from 去将一个类数组对象转成一个数组。

## 4.6 用 Array.from 而不是 ... 运算符去做map遍历。 因为这样可以避免创建一个临时数组。

## 4.7 在数组方法的回调函数中使用 return 语句。 如果函数体由一条返回一个表达式的语句组成， 并且这个表达式没有副作用， 这个时候可以忽略return

# 5.Destructuring

## 5.1 用对象的解构赋值来获取和使用对象某个或多个属性值。

Why? 解构保存了这些属性的临时值/引用

## 5.2 用数组解构.

## 5.3 多个返回值用对象的解构，而不是数据解构。

Why? 你可以在后期添加新的属性或者变换变量的顺序而不会打破原有的调用

# 6.Strings

6.1 对string用单引号 '' 。

6.2 超过100个字符的字符串不应该用string串联成多行。

Why? 被折断的字符串工作起来是糟糕的而且使得代码更不易被搜索。

6.3 用字符串模板而不是字符串拼接来组织可编程字符串。

Why? 模板字符串更具可读性、语法简洁、字符串插入参数。

6.4 永远不要在字符串中用eval()，他就是潘多拉盒子。

6.5 不要使用不必要的转义字符。

Why? 反斜线可读性差，所以他们只在必须使用时才出现哦

# 7.Functions

## 7.1 用命名函数表达式而不是函数声明。

函数表达式： const func = function () {}

函数声明： function func() {}

Why? 函数声明时作用域被提前了，这意味着在一个文件里函数很容易（太容易了）在其定义之前被引用。这样伤害了代码可读性和可维护性。如果你发现一个函数有大又复杂，这个函数妨碍这个文件其他部分的理解性，这可能就是时候把这个函数单独抽成一个模块了。别忘了给表达式显示的命名，不用管这个名字是不是由一个确定的变量推断出来的，这消除了由匿名函数在错误调用栈产生的所有假设，这在现代浏览器和类似babel编译器中很常见 (Discussion)

## 7.2 把立即执行函数包裹在圆括号里。

Why? immediately invoked function expression = IIFE

Why? 一个立即调用的函数表达式是一个单元 - 把它和他的调用者（圆括号）包裹起来，在括号中可以清晰的地表达这些。

Why? 注意：在模块化世界里，你几乎用不着 IIFE

## 7.3 不要在非函数块（if、while等等）内声明函数。把这个函数分配给一个变量。浏览器会允许你这样做，但浏览器解析方式不同，这是一个坏消息。【详见no-loop-func】 eslint: no-loop-func

7.4 Note: 在ECMA-262中 [块 block] 的定义是： 一系列的语句； 但是函数声明不是一个语句。 函数表达式是一个语句。

7.5 不要用arguments命名参数。他的优先级高于每个函数作用域自带的 arguments 对象， 这会导致函数自带的 arguments 值被覆盖

7.6 不要使用arguments，用rest语法...代替。 eslint: prefer-rest-params

Why? ...明确你想用那个参数。而且rest参数是真数组，而不是类似数组的arguments

7.7 用默认参数语法而不是在函数里对参数重新赋值。

7.8 默认参数避免副作用

7.9 把默认参数赋值放在最后

7.10 不要用函数构造器创建函数。 eslint: no-new-func

Why? 以这种方式创建函数将类似于字符串 eval()，这会打开漏洞。

7.11 函数签名部分要有空格。eslint: space-before-function-paren space-before-blocks

Why? 统一性好，而且在你添加/删除一个名字的时候不需要添加/删除空格

7.12 不要改参数. eslint: no-param-reassign

Why? 操作参数对象对原始调用者会导致意想不到的副作用。 就是不要改参数的数据结构，保留参数原始值和数据结构。

7.13 不要对参数重新赋值。 eslint: no-param-reassign

Why? 参数重新赋值会导致意外行为，尤其是对 arguments。这也会导致优化问题，特别是在V8里

7.14 用spread操作符...去调用多变的函数更好。 eslint: prefer-spread

Why? 这样更清晰，你不必提供上下文，而且你不能轻易地用apply来组成new

7.15 调用或者书写一个包含多个参数的函数应该像这个指南里的其他多行代码写法一样： 每行值包含一个参数，每行逗号结尾。

# 8.Arrow Functions

## 8.1 当你一定要用函数表达式（在回调函数里）的时候就用箭头表达式吧。 eslint: prefer-arrow-callback, arrow-spacing

Why? 他创建了一个this的当前执行上下文的函数的版本，这通常就是你想要的；而且箭头函数是更简洁的语法

Why? 什么时候不用箭头函数： 如果你有一个相当复杂的函数，你可能会把这个逻辑移出到他自己的函数声明里。

8.2 如果函数体由一个没有副作用的表达式语句组成，删除大括号和return。否则，继续用大括号和 return 语句。 eslint: arrow-parens, arrow-body-style

Why? 语法糖，当多个函数链在一起的时候好读

8.3 万一表达式涉及多行，把他包裹在圆括号里更可读。

Why? 这样清晰的显示函数的开始和结束

8.4 如果你的函数只有一个参数并且函数体没有大括号，就删除圆括号。否则，参数总是放在圆括号里。 注意： 一直用圆括号也是没问题，只需要配置 “always” option for eslint. eslint: arrow-parens

Why? 这样少一些混乱， 其实没啥语法上的讲究，就保持一个风格。

8.5 避免箭头函数(=>)和比较操作符（<=, >=）混淆. eslint: no-confusing-arrow

8.6 在隐式return中强制约束函数体的位置， 就写在箭头后面。 eslint: implicit-arrow-linebreak

# 9.classes & constructors

9.1 常用class，避免直接操作prototype

Why? class语法更简洁更易理解

9.2 用extends实现继承

Why? 它是一种内置的方法来继承原型功能而不打破instanceof

9.3 方法可以返回this来实现方法链

9.4 写一个定制的toString()方法是可以的，只要保证它是可以正常工作且没有副作用的

9.5 如果没有具体说明，类有默认的构造方法。一个空的构造函数或只是代表父类的构造函数是不需要写的。 eslint: no-useless-constructor

9.6 避免重复类成员。 eslint: no-dupe-class-members

Why? 重复类成员会默默的执行最后一个 —— 重复本身也是一个bug

# 10.Modules

10.1 用(import/export) 模块而不是无标准的模块系统。你可以随时转到你喜欢的模块系统。

Why? 模块化是未来，让我们现在就开启未来吧。

10.2 不要用import通配符， 就是 * 这种方式

Why? 这确保你有单个默认的导出

10.3 不要直接从import中直接export

Why? 虽然一行是简洁的，有一个明确的方式进口和一个明确的出口方式来保证一致性。

10.4 一个路径只 import 一次。

eslint: no-duplicate-imports

Why? 从同一个路径下import多行会使代码难以维护

10.5 不要到处可变的东西

eslint: import/no-mutable-exports

Why? 变化通常都是需要避免，特别是当你要输出可变的绑定。虽然在某些场景下可能需要这种技术，但总的来说应该导出常量。

10.6 在一个单一导出模块里，用 export default 更好。

eslint: import/prefer-default-export

Why? 鼓励使用更多文件，每个文件只做一件事情并导出，这样可读性和可维护性更好。

10.7 import 放在其他所有语句之前。

eslint: import/first

Why? 让import放在最前面防止意外行为。

10.8 多行import应该缩进，就像多行数组和对象字面量

Why? 花括号与样式指南中每个其他花括号块遵循相同的缩进规则，逗号也是。

10.9 在import语句里不允许Webpack loader语法

eslint: import/no-webpack-loader-syntax

Why? 一旦用Webpack语法在import里会把代码耦合到模块绑定器。最好是在webpack.config.js里写webpack loader语法



11.Iterators and Generators

11.1 不要用遍历器。用JavaScript高级函数代替for-in、 for-of。 eslint: no-iterator no-restricted-syntax

Why? 这强调了我们不可变的规则。 处理返回值的纯函数比副作用更容易。

Why? 用数组的这些迭代方法： map() / every() / filter() / find() / findIndex() / reduce() / some() / … , 用对象的这些方法 Object.keys() / Object.values() / Object.entries() 去产生一个数组， 这样你就能去遍历对象了。

11.2 现在不要用generator

Why? 它在es5上支持的不好

11.3 如果你一定要用，或者你忽略我们的建议, 请确保它们的函数签名空格是得当的。 eslint: generator-star-spacing

Why? function 和 * 是同一概念关键字 - *不是function的修饰符，function*是一个和function不一样的独特结构



12.Properties

## 12.1 访问属性时使用点符号. eslint: dot-notation

12.2 当获取的属性是变量时用方括号[]取

12.3做幂运算时用幂操作符 ** 。 eslint: no-restricted-properties.

13. Variables

13.1 用const或let声明变量。不这样做会导致全局变量。 我们想要避免污染全局命名空间。首长这样警告我们。 eslint: no-undef prefer-const

13.2 每个变量都用一个 const 或 let。 eslint: one-var

Why? 这种方式很容易去声明新的变量，你不用去考虑把;调换成,，或者引入一个只有标点的不同的变化。这种做法也可以是你在调试的时候单步每个声明语句，而不是一下跳过所有声明。

13.3 const放一起，let放一起

Why? 在你需要分配一个新的变量， 而这个变量依赖之前分配过的变量的时候，这种做法是有帮助的

13.4 在你需要的地方声明变量，但是要放在合理的位置

Why? let 和 const 都是块级作用域而不是函数级作用域

13.5 不要使用链接变量分配。 eslint: no-multi-assign

Why? 链接变量分配创建隐式全局变量。

13.6 不要使用一元自增自减运算符（++， --）. eslint no-plusplus

Why? 根据eslint文档，一元增量和减量语句受到自动分号插入的影响，并且可能会导致应用程序中的值递增或递减的无声错误。 使用num + = 1而不是num ++或num ++语句来表达你的值也是更有表现力的。 禁止一元增量和减量语句还会阻止您无意地预增/预减值，这也会导致程序出现意外行为。

13.7 在赋值的时候避免在 = 前/后换行。 如果你的赋值语句超出 max-len， 那就用小括号把这个值包起来再换行。 eslint operator-linebreak.



Why? 在 = 附近换行容易混淆这个赋值语句。

13.8 不允许有未使用的变量。 eslint: no-unused-vars

Why? 一个声明了但未使用的变量更像是由于重构未完成产生的错误。这种在代码中出现的变量会使阅读者迷惑。

14. Hoisting

## 14.1 var声明会被提前到他的作用域的最前面，它分配的值还没有提前。const 和let被赋予了新的调用概念时效区 —— Temporal Dead Zones (TDZ)。 重要的是要知道为什么 typeof不再安全.

14.2 匿名函数表达式和 var 情况相同

14.3 已命名函数表达式提升他的变量名，不是函数名或函数体

14.4 函数声明则提升了函数名和函数体

详情请见JavaScript Scoping & Hoisting by Ben Cherry.



15. Comparison Operators & Equality

15.1 用 === 和 !== 而不是 == 和 !=. eslint: eqeqeq

15.2 条件语句如’if’语句使用强制`ToBoolean’抽象方法来评估它们的表达式，并且始终遵循以下简单规则：

Objects 计算成 true

Undefined 计算成 false

Null 计算成 false

Booleans 计算成 the value of the boolean

Numbers

+0, -0, or NaN 计算成 false

其他 true

Strings

'' 计算成 false

其他 true

15.3 布尔值用缩写，而字符串和数字要明确比较对象

15.4 更多信息请见Angus Croll的真理、平等和JavaScript —— Truth Equality and JavaScript

15.5 在case和default分句里用大括号创建一块包含语法声明的区域(e.g. let, const, function, and class). eslint rules: no-case-declarations.

Why? 语法声明在整个switch的代码块里都可见，但是只有当其被分配后才会初始化，他的初始化时当这个case被执行时才产生。 当多个case分句试图定义同一个事情时就出问题了

15.6 三元表达式不应该嵌套，通常是单行表达式。

eslint rules: no-nested-ternary.

15.7 避免不需要的三元表达式

eslint rules: no-unneeded-ternary.

15.8 用圆括号来混合这些操作符。 只有当标准的算术运算符(+, -, *, & /)， 并且它们的优先级显而易见时，可以不用圆括号括起来。 eslint: no-mixed-operators

Why? 这提高了可读性，并且明确了开发者的意图



16.Blocks

16.1 用大括号包裹多行代码块。 eslint: nonblock-statement-body-position

16.2 if表达式的else和if的关闭大括号在一行。 eslint: brace-style

16.3 如果 if 语句中总是需要用 return 返回， 那后续的 else 就不需要写了。 if 块中包含 return， 它后面的 else if 块中也包含了 return， 这个时候就可以把 return 分到多个 if 语句块中。 eslint: no-else-return



17. Control Statements

17.1 当你的控制语句(if, while 等)太长或者超过最大长度限制的时候， 把每一个(组)判断条件放在单独一行里。 逻辑操作符放在行首。

Why? 把逻辑操作符放在行首是让操作符的对齐方式和链式函数保持一致。这提高了可读性，也让复杂逻辑更容易看清楚。

17.2 不要用选择操作符代替控制语句。



18. Comments

18.1 多行注释用 /** ... */

18.2 单行注释用//，将单行注释放在被注释区域上面。如果注释不是在第一行，那么注释前面就空一行

18.3 所有注释开头空一个，方便阅读。 eslint: spaced-comment

18.4 在你的注释前使用FIXME'或TODO’前缀， 这有助于其他开发人员快速理解你指出的需要重新访问的问题， 或者您建议需要实现的问题的解决方案。 这些不同于常规注释，因为它们是可操作的。 动作是FIXME： - 需要计算出来或TODO： - 需要实现。

18.5 用// FIXME:给问题做注释

18.6 用// TODO:去注释问题的解决方案



19. Whitespace

19.1 tab用两个空格. eslint: indent

19.2 在大括号前空一格。 eslint: space-before-blocks

19.3 在控制语句(if, while 等)的圆括号前空一格。在函数调用和定义时，参数列表和函数名之间不空格。 eslint: keyword-spacing

19.4 用空格来隔开运算符。 eslint: space-infix-ops

19.5 文件结尾空一行. eslint: eol-last

19.6 当出现长的方法链（>2个）时用缩进。用点开头强调该行是一个方法调用，而不是一个新的语句。eslint: newline-per-chained-call no-whitespace-before-property

19.7 在一个代码块后下一条语句前空一行。

19.8 不要用空白行填充块。 eslint: padded-blocks

19.9不要在代码之间使用多个空白行填充。 eslint: no-multiple-empty-lines

19.10 圆括号里不要加空格。 eslint: space-in-parens

19.11 方括号里不要加空格。看示例。 eslint: array-bracket-spacing

19.12 花括号里加空格。 eslint: object-curly-spacing

19.13 避免一行代码超过100个字符（包含空格）。

注意： 对于上面——strings–line-length，长字符串不受此规则限制，不应分解。 eslint: max-len

Why? 这样确保可读性和可维护性

19.14 作为语句的花括号内也要加空格 —— { 后和 } 前都需要空格。 eslint: block-spacing

19.15 , 前不要空格， , 后需要空格。 eslint: comma-spacing

19.16 计算属性内要空格。参考上述花括号和中括号的规则。 eslint: computed-property-spacing

19.17 调用函数时，函数名和小括号之间不要空格。 eslint: func-call-spacing

19.18 在对象的字面量属性中， key value 之间要有空格。 eslint: key-spacing

19.19 行末不要空格。 eslint: no-trailing-spaces

19.20 避免出现多个空行。 在文件末尾只允许空一行。 eslint: no-multiple-empty-lines



20. Commas

20.1 不要前置逗号。 eslint: comma-style

20.2 额外结尾逗号: 要 eslint: comma-dangle



Why? 这导致git diffs更清洁。 此外，像Babel这样的转换器会删除转换代码中的额外的逗号，这意味着你不必担心旧版浏览器中的结尾逗号问题。



21. Semicolons

21.1 Yup. eslint: semi



Why? 当 JavaScript 遇到没有分号结尾的一行，它会执行自动插入分号 Automatic Semicolon Insertion这一规则来决定行末是否加分号。如果JavaScript在你的断行里错误的插入了分号，就会出现一些古怪的行为。当新的功能加到JavaScript里后， 这些规则会变得更复杂难懂。显示的结束语句，并通过配置代码检查去捕获没有带分号的地方可以帮助你防止这种错误。

Read more.



22. Type Casting & Coercion

22.1 在语句开始执行强制类型转换。

22.2 Strings: eslint: no-new-wrappers

22.3 Numbers: 用 Number 做类型转换，parseInt转换string常需要带上基数。 eslint: radix

22.4 请在注释中解释为什么要用移位运算和你在做什么。无论你做什么狂野的事，比如由于 parseInt 是你的性能瓶颈导致你一定要用移位运算。 请说明这个是因为性能原因,

22.5 注意: 用移位运算要小心. 数字使用64-位表示的，但移位运算常常返回的是32为整形source)。移位运算对大于32位的整数会导致意外行为。Discussion. 最大的32位整数是 2,147,483,647:

22.6 布尔:



23. Naming Conventions

23.1 避免用一个字母命名，让你的命名可描述。 eslint: id-length

23.2 用小驼峰式命名你的对象、函数、实例。 eslint: camelcase

23.3 用大驼峰式命名类。 eslint: new-cap

23.4 不要用前置或后置下划线。 eslint: no-underscore-dangle



Why? JavaScript 没有私有属性或私有方法的概念。尽管前置下划线通常的概念上意味着“private”，事实上，这些属性是完全公有的，因此这部分也是你的API的内容。这一概念可能会导致开发者误以为更改这个不会导致崩溃或者不需要测试。 如果你想要什么东西变成“private”，那就不要让它在这里出现。

23.5 不要保存引用this， 用箭头函数或函数绑定——Function#bind.

23.6 export default导出模块A，则这个文件名也叫A.*， import 时候的参数也叫A。 大小写完全一致。

23.7 当你export-default一个函数时，函数名用小驼峰，文件名需要和函数名一致。

23.8 当你export一个结构体/类/单例/函数库/对象 时用大驼峰。

23.9 简称和缩写应该全部大写或全部小写。



Why? 名字都是给人读的，不是为了适应电脑的算法的。

23.10 你可以用全大写字母设置静态变量，他需要满足三个条件。

导出变量

是 const 定义的， 保证不能被改变

这个变量是可信的，他的子属性都是不能被改变的



Why? 这是一个附加工具，帮助开发者去辨识一个变量是不是不可变的。

对于所有的 const 变量呢？ —— 这个是不必要的。大写变量不应该在同一个文件里定义并使用， 它只能用来作为导出变量。 赞同！

那导出的对象呢？ —— 大写变量处在export的最高级(e.g. EXPORTED_OBJECT.key) 并且他包含的所有子属性都是不可变的。



24. Accessors

24.1 不需要使用属性的访问器函数。

24.2 不要使用JavaScript的getters/setters，因为他们会产生副作用，并且难以测试、维护和理解。相反的，你可以用 getVal()和setVal(‘hello’)去创造你自己的accessor函数

24.3 如果属性/方法是boolean， 用 isVal() 或 hasVal()

24.4 用get()和set()函数是可以的，但是要一起用



25. Events

25.1 通过哈希而不是原始值向事件装载数据时(不论是DOM事件还是像Backbone事件的很多属性)。 这使得后续的贡献者（程序员）向这个事件装载更多的数据时不用去找或者更新每个处理器



26. jQuery

26.1 jQuery对象用$变量表示。

26.2 暂存jQuery查找

26.3 DOM查找用层叠式$('.sidebar ul') 或 父节点 > 子节点 $('.sidebar > ul'). jsPerf

26.4 用jQuery对象查询作用域的find方法查询

