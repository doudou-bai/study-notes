# Java新特性

## Java8

### Lambda表达式

格式

```
-> :Lambda操作符 或 箭头操作符
-> 左边 Lambda形参列表
-> 右边 Lambda体
```

原始代码

```java
 Runnable r1 = new Runnable() {
            @Override
            public void run() {
                System.out.println("我爱天安门");
            }
        };
```

Lambda代码

```java
  Runnable r2 = () -> System.out.println("我爱北京");
  r2.run();
```

代码格式

```java
package Java8.Lombda;

import org.junit.Test;

import java.util.Comparator;
import java.util.function.Consumer;

/**
 * Create By 王嘉浩
 * Time 2021/5/25 14:23
 */
public class LambdaTest1 {
    //无参无返回值
    @Test
    public void test1() {
        Runnable r1 = () -> System.out.println("无参无返回值");
        r1.run();
    }

    //Lambda需要一个参数,但是没有返回值
    @Test
    public void test2() {
        Consumer<String> c1 = (String a) -> System.out.println(a);
        c1.accept("Lambda需要一个参数,但是没有返回值");
    }

    //数据类型可以省略
    @Test
    public void test3() {
        Consumer<String> c1 = (a) -> System.out.println(a);
        c1.accept("Lambda需要一个参数,但是没有返回值");
    }

    //Lambda只需要一个参数的时候小括号可以省略
    @Test
    public void test4() {
        Consumer<String> c1 = a -> System.out.println(a);
        c1.accept("Lambda需要一个参数,但是没有返回值");
    }

    //Lambda只需要两个及以上参数的时候 可以 有返回值 多条执行语句
    @Test
    public void test5() {
        Comparator<Integer> com1 = (s1, s2) -> {
            System.out.println(s1);
            System.out.println(s2);
            return s1.compareTo(s2);
        };
        int compare = com1.compare(1, 2);
        System.out.println(compare);
    }
    //Lambda只有一条语句 return与大括号若有 都可以省略
    @Test
    public void test6() {
        Comparator<Integer> com1 = (s1, s2) -> s1.compareTo(s2);
        int compare = com1.compare(1, 2);
        System.out.println(compare);
    }
}

```

### 函数式接口

如果一个接口中,只声明一个抽象方法,那这个接口就是函数式接口 

注解

```
@FunctionalInterface
```

### 方法引用

方法引用可以看做是Lambda表达式深层次的表达

方法引用使用要求:要求接口中的抽象方法的形参列表和返回值类型与方法引用的形参列表和返回值类型相同 

代码

```java
package Java8.method;

import Java8.Lombda.MyInterdace;
import org.junit.Test;

import java.io.PrintStream;
import java.util.Comparator;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Supplier;

/**
 * Create By 王嘉浩
 * Time 2021/5/25 22:07
 */
public class MethodRefTest {
    @Test
    public void test1() {
        //Lambda
        Consumer<String> com1 = str -> System.out.println(str);
        com1.accept("北京");
        //方法引用
        Consumer<String> com2 = System.out::println;
        com2.accept("南京");
    }

    @Test
    public void test2() {
        //Lambda
        Employee employee = new Employee(1001, "Tom", 23, 5600);
        Supplier<String> sup1 = () -> employee.getName();
        System.out.println(sup1.get());
        //方法引用
        Supplier<String> sup2 = employee::getName;
        System.out.println(sup2.get());
    }

    @Test
    public void test3() {
        //Lambda
        Comparator<Integer> com1 = (t1, t2) -> Integer.compare(t1, t2);
        System.out.println(com1.compare(1, 2));
        //方法引用
        Comparator<Integer> com2 = Integer::compare;
        System.out.println(com2.compare(2, 1));
    }

    @Test
    public void test4() {
        //Lambda
        Function<Double, Long> func1 = d -> Math.round(d);
        System.out.println(func1.apply(10D));
        //方法引用
        Function<Double, Long> func2 =  Math::round;
        System.out.println(func2.apply(20d));
    }
}
```

https://www.bilibili.com/video/BV184411x7XA?p=10&spm_id_from=pageDriver