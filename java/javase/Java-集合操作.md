

# 常用的Stream转换

## List< Integer >  转  Integer[]

不涉及unboxed操作

```java
public class Stream {
	 
  public static void main(String[] args) {
		
    // String或其他referent type可用转换方法  e.g. List<Integer> => Integer[]
    List<String> list = new ArrayList<>(List.of("a", "b", "c"));
    String[] strs = list.toArray(new String[0]);
    System.out.println(Arrays.toString(strs));

    ArrayList<Integer> list1 = new ArrayList<>(List.of(1, 2, 3));
    Integer[] integers = list1.toArray(new Integer[0]);
    // or list1.toArray(Integer[]::new);
    System.out.println(Arrays.toString(integers));
  }
}
```





## List< Integer >  转  int[]

涉及unboxed操作

```java
public class Stream {

  public static void main(String[] args) {
    // List<Integer> => int[] 转换
    int[] ints = list1.stream()
                      .mapToInt(Integer::intValue)
                      .toArray();
    System.out.println(Arrays.toString(ints));

    // int[] => List<Integer>
    int[] origin = new int[] {1, 2, 3, 4, 5, 6};
    List<Integer> list2 = Arrays.stream(origin)
                                  .boxed()
                                  .collect(Collectors.toList());
		
    // int[] => Integer[]
    Integer[] integers1 = Arrays.stream(origin)
                                .boxed()
                                .toArray(Integer[]::new);


  }
}
```



## int[] 转 List< Integer >

```java
public class Stream {

  public static void main(String[] args) {
    // int[] => List<Integer>
    int[] origin = new int[] {1, 2, 3, 4, 5, 6};
    List<Integer> list2 = Arrays.stream(origin)
                                  .boxed()
                                  .collect(Collectors.toList());	
  }
}
```



## int[] 转 Integer[]

```java
public class Stream {
    // int[] => Integer[]
    Integer[] integers1 = Arrays.stream(origin)
                                .boxed()
                                .toArray(Integer[]::new);

  }
}
```









# 迭代器中进行remove

```java
public class RemoveTest {

    static HashMap<String, Integer> map = new HashMap<>();
    static {
        map.put("1", 1);
        map.put("2", 2);
        map.put("3", 3);
        map.put("4", 4);
    }

    public static void main(String[] args) {
  //    	for (Integer val : map.values()) {    常见的ConcurrentModificationException写法
  //          map.remove(String.valueOf(val));
  //      }
      
        for (Integer val : map.values().toArray(new Integer[0])) {  // 使用新生成的数组对象进行迭代,就不会报错
            map.remove(String.valueOf(val));
        }
    }
}
```







