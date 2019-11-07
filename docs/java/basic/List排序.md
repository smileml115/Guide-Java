# 简单排序
```java
List<Integer> list = new ArrayList<Integer>();
list.add(8);
list.add(6);
list.add(12);
//list.sort(null);//also be realized
Collections.sort(list);
System.out.println(list.toString());
```
程序运行结果：

[6, 8, 12]，这种简单的排序直接按照自然顺序进行升序排列。

# 泛型使用Comparable接口
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Test {

	public static void main(String[] args) {
		List<User> list = new ArrayList<User>();
		list.add(new User("张三", 5));
		list.add(new User("李四", 30));
		list.add(new User("王五", 19));
		list.add(new User("陈十七", 17)); 
		//list.sort(null);//also be realized
		Collections.sort(list);
		System.out.println(list.toString());
	}

	static class User implements Comparable<User> {

		private String name; // 姓名

		private int age; // 年龄

		public User(String name, int age) {
			this.name = name;
			this.age = age;
		}

		// getter && setter
		public String getName() {
			return name;
		}

		public void setName(String name) {
			this.name = name;
		}

		public int getAge() {
			return age;
		}

		public void setAge(int age) {
			this.age = age;
		}

		@Override
		public String toString() { // 重写toString
			return "User [name=" + name + ", age=" + age + "]";
		}

		@Override
		public int compareTo(User user) { // 重写Comparable接口的compareTo方法，
			return this.age - user.getAge();// 根据年龄升序排列，降序修改相减顺序即可
		}
	}
}

```
程序运行结果：根据年龄升序排列

[User [name=张三, age=5], User [name=陈十七, age=17], User [name=王五, age=19], User [name=李四, age=30]]

# 匿名内部类实现排序
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class Test {

	public static void main(String[] args) {
		List<User> list = new ArrayList<User>();
		list.add(new User("张三", 5));
		list.add(new User("李四", 30));
		list.add(new User("王五", 19));
		list.add(new User("陈十七", 17)); // 陈十七永远十七岁
//		list.sort(new Comparator<User>() {
//			@Override
//			public int compare(User u1, User u2) {
//				int diff = u1.getAge() - u2.getAge();
//				if (diff > 0) {
//					return 1;
//				} else if (diff < 0) {
//					return -1;
//				}
//				return 0; // 相等为0
//			}
//		}); // 按年龄排序
		Collections.sort(list, new Comparator<User>() {
			@Override
			public int compare(User u1, User u2) {
				int diff = u1.getAge() - u2.getAge();
				if (diff > 0) {
					return 1;
				} else if (diff < 0) {
					return -1;
				}
				return 0; // 相等为0
			}
		}); // 按年龄排序
		System.out.println(list.toString());
	}

	static class User implements Comparable<User> {

		private String name; // 姓名

		private int age; // 年龄

		public User(String name, int age) {
			this.name = name;
			this.age = age;
		}

		// getter && setter
		public String getName() {
			return name;
		}

		public void setName(String name) {
			this.name = name;
		}

		public int getAge() {
			return age;
		}

		public void setAge(int age) {
			this.age = age;
		}

		@Override
		public String toString() {
			return "User [name=" + name + ", age=" + age + "]";
		}

		@Override
		public int compareTo(User user) { // 重写Comparable接口的compareTo方法，
			return this.age - user.getAge();// 根据年龄升序排列，降序修改相减顺序即可
		}
	}
}

```

 运行结果：[User [name=张三, age=5], User [name=陈十七, age=17], User [name=王五, age=19], User [name=李四, age=30]]