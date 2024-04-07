## Data Structure.

- It is the way by which we can store the data in a efficient way.

- It is mainly used to reduce the space and time complexity of the task.

### Types of Data Structure.

![alt text](image.png)

**Primitive data structure**

- Primitive data structure is a fundamental type of data structure that stores the data of only one type 

- For smaller application we can use primitive data structure. For example - Calculation or snake game.

**Non-primitive data structure** 

- Non-primitive data structure is a type of data structure which is a user-defined that stores the data of different types in a single entity.

- For large application we need to use non-primitive data structure as we need lots of data in a single object and for faster retrieval and deletion of data we also need algorithm in this type of application. For example ecommerce website.


## Difference between Arrays and Collections.

### Arrays
- Arrays can store both primitive and non-primitive data.

```java
int[] a = {1,2,3,4}//Primitive data type
class Test{

}
Test [] t = {obj1, obj2, obj3, obj4}//Non-primitive data type
```
- Arrays can store only homogeneous type of data.

- Arrays size is fixed we cannot increase or decrease the size of an array at runtime.

- Arrays are inbuilt features of java and thus we need to develop algorithm for insertion and deletion.


### Collection Framework

- Collection framework can store only non-primitive type of data.

```java
ArrayList al = new ArrayList();
al.add(obj1);//Non primitive data 
al.add(10);//Non primitive data as it will store this value as object.
```
- Collection can store only heterogeneous type of data.

- Collection size is not fixed we can increase or decrease the size of the collections at runtime.

- Collection framework is an API which provides pre defined classes interfaces and methods.

## Collection Framework.

- It is the set of predefined classes and interface which is used to store multiple data.

- It contains 2 main parts.

  - java.util.Collection

  - ![alt text](image-1.png)

  - java.util.Map

  - ![alt text](image-2.png)

**What is Collection Framework, Collection and Collections?**

**Collection Framework(API)** - It is an API which contain predefined classes and interfaces.

**Collection(Interface)** - It is the root interface(present in java.util.package) of all the collection objects

**Collections(Utility Class)**. - It is the utility class which contain only static method. 


### Collection framework hierarchy

![alt text](image-3.png)

## Collection Interface.

- Collection is an interface which is present in java.util.package

- Syntax ```public interface Collection <E> extends Interable<E>```

- Hierarchy of Collection

![alt text](image-4.png)

- Methods of Collection

  - ```public boolean add(Object obj)```
  ```java
  ArrayList al = new ArrayList();
  al.add(10);//adding object in collection 
  al.add(20);
  System.out.println(al.add(30))//It will return boolean value which is true that means the value is added in the collection.
  ```

  - ```public boolean addAll(Collection c)```

  ```java
  ArrayList ak = new ArrayList();
  ak.add(al)//Adding collection in other collection
  ```

  -```public boolean remove(Object obj)```

  ```java
  ArrayList al = new ArrayList();
  al.add(10);//adding object in collection 
  al.add(20);
  ak.remove(0)//We have to provide the index value in the remove method the value 10 will get deleted 
  ```

  -```public boolean removeAll(Collection c)```

  ```java
   ArrayList al = new ArrayList();
  al.add(10);
  al.add(20);
  al.add(34);
  al.add(44);
  ArrayList ak = new ArrayList();
  ak.add('a');
  ak.add('b');
  ak.add('c');
  al.addAll(ak);
  System.out.println(al);
  al.removeAll(ak);
  System.out.println(al);

  ```

  -```void clear()```

  ```java
  ArrayList al = new ArrayList();
  al.add(10);
  al.add(20);
  al.add(34);
  al.add(44);
  al.clear();
  System.out.println(al);
  ```

  -```boolean contains(Object obj)```

  ```java
  ArrayList al = new ArrayList();
  al.add(10);//adding object in collection 
  al.add(20);
  System.out.println(al.contains(10))//It will print true
  ```

  -```boolean containsAll(Collection c)```

  ```java
   ArrayList al = new ArrayList();
  al.add(10);
  al.add(20);
  al.add(34);
  al.add(44);
  ArrayList ak = new ArrayList();
  ak.add('a');
  ak.add('b');
  ak.add('c');
  al.addAll(ak);
  System.out.println(al.containsAll(ak));
  ```

  -```boolean isEmpty()```

  ```java
  ArrayList al = new ArrayList();
  System.out.println(al.isEmpty());//It will return false as there is no object in al collection
  ```

  -```int size()```

  ```java
  ArrayList al = new ArrayList();
  al.add(1);
  al.add(2);
  al.add(3);
  System.out.println(al.size());//It will return 3 
  ```

  -```Iterator iterator()```



## Difference between set and list.

### list

- List in an indexed based data structure.

- List can store duplicate element.

- List can store any number of null values.

- List follows the insertion order.

- We can iterate the list element by Iterator and ListIterator.


```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
public class ListDemo{
    public static void main(String args[]){
        List l = new ArrayList();
        l.add(10);//It is a indexed based data structure value is store in a sequence wise
        l.add(20);
        l.add(20);//We can add duplicate value in list
        l.add(null);
        l.add(null);//We can add multiple null value
        Iterator itr = l.iterator();//Here we can use ListIterator interface also to iterate through the collection
        while(itr.hasNext()){
            System.out.println(itr.next());
        }
    }
}
```

### set

- Set is not an indexed based data structure. It stores the data according to the hashcode values.

- Set does not allow to store duplicate element.

- Set can store only one null value.

- We can iterate the set element by Iterator only.

- Set does not follow the insertion order.

```java
import java.util.HashSet;
import java.util.Set;
public class SetDemo{
    public static void main(String args[]){
       Set s = new HashSet();
       s.add(3);
       s.add(4);//It is not an indexed based data structure that means value is not stored in a sequence wise.
       s.add(4);//We cannot add duplicate value in set
       s.add(null);
       s.add(null);//We cannot store null values as it dont allow duplicacy
        Iterator itr = s.iterator();//Here there is no ListIterator only Iterator
        while(itr.hasNext()){
            System.out.println(itr.next());
        }
    }
}

```