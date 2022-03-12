## 1.optional
Optional.ofNullable(model.getLinkModels()).ifPresent


of(value) get()都会报npe,

orElse(如果这里面是方法，都会执行的)

 `Optional`属于返回类型，在业务返回值或者远程调用中使用 

| ab                             | bb                                                           |
| ------------------------------ | ------------------------------------------------------------ |
| empty()                        | 返回一个`Optional`容器对象                                   |
| isPresent()                    | 判断`Optional`中是否有值，返回 boolean                       |
| ofNullable(T value)            | 创建一个`Optional`对象，但 value 为空时返回`Optional.empty()` |
| orElseGet(supplier)            | 取不到值时返回默认值                                         |
| orElseThrow(exceptionSupplier) | 阻塞性业务场景推荐使用,例如没有从上游获取到信息，下面的所有操作都无法进行 |
| ifPresent(consumer)            | 有值则执行 consumer，否则什么都不干                          |


## 2.localdatetime
**都是****final****类**

> localdate

| LocalDate.now()                      |      |
| ------------------------------------ | ---- |
| LocalDate.of(2021,8,1)               |      |
| int  localDate.getYear()             |      |
| int  localDate.getMonth().getValue() |      |
| int  localDate.getDayOfWeek()        |      |

> localtime

| LocalTime.now()            |      |
| -------------------------- | ---- |
| LocalTime.of(10,8,8)       |      |
| int  localTime.getHour()   |      |
| int  localTime.getMinute() |      |
| int  localTime.getSecond() |      |

> localdatetime

| LocalDateTime  LocalDateTime.of(localdate,localtime)         |                       |
| ------------------------------------------------------------ | --------------------- |
| 转换                                                         | at/to                 |
| LocalDateTime  localDate.atTime(localtime)                   |                       |
| LocalDate localDateTime.toLocalDate()                        |                       |
| 增加、减少                                                   | plus/minus            |
| localDateTime.plus(1, **ChronoUnit**.YEARS)                  |                       |
| localDateTime.plusYear(1)                                    |                       |
| 指定修改                                                     | with                  |
| localDateTime.withYear(2020)                                 |                       |
| localDateTime.with(ChronoField.YEAR, 2022)                   |                       |
| 时间计算                                                     |                       |
| LocalDate.*now*().  with(**TemporalAdjusters**.*previous*(DayOfWeek.*SUNDAY*)).plusDays(1); | 这周一，previous/next |
| 具体看API                                                    |                       |
| 格式化/解析                                                  | 线程安全              |
| DateTimeFormatter  dtf = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");  dtf.format(time);  LocalDateTime.parse(strDate3,dtf) |                       |

## 3.lambda
1.Lambda表达式
	​ (形式参数) -> {代码块}
	Lambda表达式的使用前提--函数式接口
	“可推导就是可省略”
	如果参数有且仅有一个，那么小括号可以省略
	如果代码块的语句只有一条，可以省略大括号和分号，和return关键字
	Lambda表达式和匿名内部类的区别
		○ 所需类型不同
	匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
		○ 实现原理不同
	匿名内部类：编译之后，产生一个单独的.class字节码文件
	Lambda表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会在运行的时候动态生成
2.引用运算符::
	对象（可以用this代替）::方法（对象就是参数）
	类::方法（无参）
	类::new
3.语法糖
指B格式是在A格式的基础上简化代码，B就是A的语法糖



## 4.函数式接口


有且仅有一个抽象方法的接口
 @FunctionalInterface

*Supplier接口*
 Supplier<T>接口也被称为生产型接口，如果我们指定了接口的泛型是什么类型，那么接口中的get方法就会生产什么类型的数据供我们使用。

| T get() | 按照某种实现逻辑(由Lambda表达式实现)返回一个数据 |
| ------- | ------------------------------------------------ |
|         |                                                  |

**Consumer接口**
 Consumer<T>接口也被称为消费型接口，它消费的数据的数据类型由泛型指定

| void accept(T t)                             | 对给定的参数执行此操作                                      |
| -------------------------------------------- | ----------------------------------------------------------- |
| default  Consumer<T> andThen(Consumer after) | 返回一个组合的Consumer，依次执行此操作，然后执行  after操作 |

**Predicate接口**
 Predicate<T>接口通常用于判断参数是否满足指定的条件

| boolean test(T t)                          | 对给定的参数进行判断(判断逻辑由Lambda表达式实现)，返回一个布尔值 |
| ------------------------------------------ | ------------------------------------------------------------ |
| default  Predicate<T> negate()             | 返回一个逻辑的否定，对应逻辑非                               |
| default  Predicate<T> and(Predicate other) | 返回一个组合判断，对应短路与                                 |
| default  Predicate<T> or(Predicate other)  | 返回一个组合判断，对应短路或                                 |

pre1.and(pre2).test(t);

**Function接口**

Function<T,R>接口通常用于对参数进行处理，**转换(**处理逻辑由Lambda表达式实现)，然后返回一个新的值

| R apply(T t)                                  | 将此函数应用于给定的参数                                     |
| --------------------------------------------- | ------------------------------------------------------------ |
| default <V>  Function andThen(Function after) | 返回一个组合函数，首先将该函数应用于输入，然后将after函数应用于结果 |

fun1.andThen(fun2).apply(t);

## 5.stream流操作
1.常用的stream三种创建方式

集合 Collection.stream()

静态方法 Stream.of("a", "b", "c")/or (arr)

数组 Arrays.stream(arr)

Map体系集合转成Set集合，间接的生成流



> 中间操作方法

 

| Stream<T> **filter**(Predicate predicate)                    |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Stream<T>  **limit**(long maxSize)                           | 截取前几个数据                                               |
| Stream<T>  **skip**(long n)                                  | 跳过前面几个，返回剩下的                                     |
| static  <T> Stream<T> **concat**(Stream a,  Stream b)        |  合并a和b两个流为一个流，Stream.of()有可以合并流？？ |
| Stream<T>  **distinct**()                                    | 通过流所生成元素的equals和hashCode去重                       |
| Stream<T>  **sorted**()                                      |                                                              |
| Stream<T>  sorted(Comparator comparator)                     |                                                              |
| <R>  Stream<R> **map**(Function mapper)                      | 接收流中元素，并且将其映射成为新元素                         |
|  flatmap | 多个流合并后map   Stream.of(basketballClub, pingpongClub,  computerClub) .flatMap(e -> e.stream().filter(s -> s.getAge() < 17)) |
|  peek(Consumer c) | 获取流中元素，操作流中元素，与foreach不同的是不会截断流，可继续操作流 |

booelan allMatch(Predicate) 都符合

boolean anyMatch(Predicate) 任一元素符合

boolean noneMatch(Predicate) 都不符合 

 

> 终结操作方法

| void forEach(Consumer  action) |      |
| ------------------------------ | ---- |
| long count()                   |      |

 

> 收集操作

 

| R collect(Collector collector) | 把结果收集到集合中 |
| ------------------------------ | ------------------ |
|                                |                    |

工具类Collectors提供了具体的收集方式

| public static  <T> Collector toList()                        | 把元素收集到List集合中 |
| ------------------------------------------------------------ | ---------------------- |
| public static  <T> Collector toSet()                         | 把元素收集到Set集合中  |
| public static  Collector toMap(Function keyMapper,Function valueMapper) | 把元素收集到Map集合中  |

 

Collectors

grouping by 分组

Map<String, List<Student>> collect = pingpongClub.stream().collect(Collectors.groupingBy(Student::getClassNum));

joining 字符串拼接（ 第一个参数是分隔符 第二个参数是前缀 第三个参数是后缀 ）

String collect4 = pingpongClub.stream().map(Student::getName).collect(Collectors.joining(",", "【", "】"));