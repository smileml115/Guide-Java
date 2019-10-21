[TOC]

# java.util.Objects

## 判断两个对象的值是否相等
`Objects.equals(Object a, Object b)`


# java.util.Arrays

## 将一个数组转换为一个List集合。

### 实现方式
`Arrays.asList(Array[])`
```java
// 方式一
String[] myArray = { "Apple", "Banana", "Orange" };
List<String> myList = Arrays.asList(myArray);
// 方式二
List myList = Arrays.asList("Apple", "Banana", "Orange");	
```

### 注意事项

**用`Arrays.asList()`将数组转换为集合后,底层其实还是数组**
![注意](/docs/image/java/UtilClass/阿里巴巴Java开发手-Arrays.asList()方法.png)

**传递的数组必须是对象数组，而不是基本类型。** 

`Arrays.asList()`是泛型方法，传入的对象必须是对象数组。

```java
int[] myArray = { 1, 2, 3 };
List myList = Arrays.asList(myArray);
System.out.println(myList.size());//1
System.out.println(myList.get(0));//数组地址值
System.out.println(myList.get(1));//报错：ArrayIndexOutOfBoundsException
int [] array=(int[]) myList.get(0);
System.out.println(array[0]);//1
```
当传入一个原生数据类型数组时，`Arrays.asList()` 的真正得到的参数就不是数组中的元素，而是数组对象本身！此时List 的唯一元素就是这个数组，这也就解释了上面的代码。

我们使用包装类型数组就可以解决这个问题。

```java
Integer[] myArray = { 1, 2, 3 };
```

### 正确的将数组转换为ArrayList

**1. 最简便的方法**

```java
List list = new ArrayList<>(Arrays.asList("a", "b", "c"))
```

**2. 使用 Java8 的Stream**

```java
Integer [] myArray = { 1, 2, 3 };
List myList = Arrays.stream(myArray).collect(Collectors.toList());
//基本类型也可以实现转换（依赖boxed的装箱操作）
int [] myArray2 = { 1, 2, 3 };
List myList = Arrays.stream(myArray2).boxed().collect(Collectors.toList());
```
  
# java.util.Collections

## 集合顺序反转
`Collections.reverse(List list);`
搭配数组→集合→反转→数组的处理可以快速实现数组的反转。
```java
String [] s= new String[]{
    "dog", "lazy", "a", "over", "jumps", "fox", "brown", "quick", "A"
};
List<String> list = Arrays.asList(s);
Collections.reverse(list);
s=list.toArray(new String[0]);
```
由于JVM优化，`new String[0]`作为`Collection.toArray()`方法的参数现在使用更好，`new String[0]`就是起一个模板的作用，指定了返回数组的类型，0是为了节省空间，因为它只是为了说明返回的类型。
