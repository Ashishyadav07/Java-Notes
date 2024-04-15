## Strings

- String is a non primitive data type because it references a memory location where data is stored in the heap memory(String constant pool) i.e, it references to a memory where object is actually placed. Thus the variable of non-primitive data type is also called reference data type and object reference variable. The object variable lives in the stack memory and the object to which it provides always lives on the heap memory. The stack holds a pointer to the object on the heap. Thus all non-primitive data types are simply called objects which are created by instantiating a class.

- String is a sequence of characters(Array of characters).
 
   ```java
    char[] c = {'a','s','h','i','s','h'};//charSequence is an interface to represent character.
    String s = new String(c);
   ```

- String is a class.

   **Syntax**

   ```java
   public final class String extends Object implements Serializable, Comparable<String>, CharSequence{
    //methods
    }
   ```
- String is an immutable object

  ```java
  String s = new String();//It is an immutable object.
  ```
- To create string there are 3 classes.

  - String
  - StringBuffer
  - StringBuilder

## String Constant Pool

- Till 1.6 version string constant pool was in method area. After 1.7 version string constant pool is in heap area because in method area the size was constant but in heap area we can increase or decrease the size of string constant pool.

- How string constant pool works?

  - using new keyword

  ```java
  String str = new String("Ashish");
  ```
  When using new keyword 2 objects are created one in heap memory and other in the string constant pool.When we use the new keyword with a string literal in the constructor (e.g., new String("hello")), it always creates a new string object in the heap memory, regardless of whether an identical string already exists in the constant pool. This means that even if the string "hello" is already present in the string constant pool, using new String("hello") will create a new object in the heap.
 
  - using string literal

   ```java
    String str = "Hello"'
   ```
   When using string constant pool only 1 objects are created in the String constant pool.The string constant pool is a special area of memory where string literals are stored. When you create a string literal using double quotes (e.g., "hello"), Java checks if a string with the same value already exists in the string constant pool. If it does, the new string literal refers to the existing string object. If not, a new string object is created in the pool.

   ![alt text](image.png)

   String Constant pool is not applicable for Garbage Collection as JVM internally creates reference variable for each string literal object.

## String immutable?

- A String is an unavoidable type of variable while writing any application program. String references are used to store various attributes like username, password, etc. In Java, String objects are immutable. Immutable simply means unmodifiable or unchangeable.

- Once String object is created its data or state can't be changed but a new String object is created.

```java

class Testimmutablestring{  
 public static void main(String args[]){  
   String s="Sachin";  
   s.concat(" Tendulkar");//concat() method appends the string at the end  
   System.out.println(s);//will print Sachin because strings are immutable objects  
 }  
}  

```
![alt text](image-1.png)

- But if we explicitly assign it to the reference variable, it will refer to "Sachin Tendulkar" object.

```java
class Testimmutablestring1{  
 public static void main(String args[]){  
   String s="Sachin";  
   s=s.concat(" Tendulkar");  
   System.out.println(s);  
 }  
}  

```
### Why String objects are immutable in java??

Strings are immutable in java because string objects are cached in String pool. Sinced cached String literals are shared between multiple person there is a risk, when one person action would affect all other persons, if one person changes its city from "Mohali" to "Delhi", all other person will also get affected.

![alt text](image-2.png)

### Important features of String class.

- **String Constant Pool** - It is a special memory area in heap area which stores string literal.

- **Immutable Objects** - The string objects are immmutable which means once string object is created its data or state can't be changed but a new string object is created.

- **+ Operator of String** - Multiple strings can be concatinated using + operator.

- **Security** - The parameters used for network connection, database connection URLs usernames/passwords etc are represented in Strings. If it was mutable, these paramters could be changes easily.

- **Class Loading** - String is used as an argument for class loading. If mutable, it could resist in the wrong class being loaded(because mutable object change their state).

- **Synchronization and Concurrency** - Making string immutable automatically makes them thread safe thereby solving the synchronization issues.

- **Memory management** - When compiler optimizes String objects, it seems that if two objects have the same value (a = "test" and b = "test") and thus we need only one string object(for both a and b , these two will point to the same object).

## Why String class are final?

The reason behind the String class being final is because no one can override the methods of the String class. So that it can provide the same features to the new String objects as well as to the old ones.

### Difference between final and immutable.

- final means that you can’t change the object’s reference to point to another reference or another object, but you can still mutate its state (using setter methods e.g). Whereas immutable means that the object’s actual value can’t be changed, but you can change its reference to another one.

- final modifier is applicable for variable but not for objects, Whereas immutability applicable for an object but not for variables.

- By declaring a reference variable as final, we won’t get any immutability nature, Even though reference variable is final. We can perform any type of change in the corresponding Object. But we can’t perform reassignment for that variable.

- final ensures that the address of the object remains the same whereas the Immutable suggests that we can’t change the state of the object once created.

Example - 

```java
final String name = "John";
name = "Same";//It will give compile error as we cant change the object reference.

String name = "John";
name = "Sam"; //We can change the object reference but can't mutate the object.
```

## Difference between == operator and equals() method.

```java
public class StringComparisonExample {  
    public static void main(String[] args) {  
        String word1 = "Java";  
        String word2 = "Java";  
        String word3 = new String("Java");  
  
        System.out.println(word1 == word2);       // Output: true  //It will print true as both the object is refering to the same object in String constant Pool
        System.out.println(word1 == word3);       // Output: false  //It will print false because one is pointing to the object in SCM and other in heap memory which was created by new keyword.
  
        System.out.println(word1.equals(word2));  // Output: true  
        System.out.println(word1.equals(word3));  // Output: true  
    }  
}  
```
![alt text](StringComparison.drawio.png)

**Equality operator(==)**

When used to compare strings, the equality operator compares the references (memory addresses) of the string objects rather than their contents. It determines whether two string objects refer to the exact same memory location. It returns true if the references are identical, meaning they point to the same memory address, and false if they do not.

**.equals() Method**
- It is a method of Object class.

- The .equals() method in Java is defined in the Object class, which is the root class for all objects in Java. It compares the content (values) of two objects for equality. 

### equals method in object class and string class.

```java
class Object{
    //11 methods in object class 
    public boolean equals(Object obj){
        return(this === obj);
    }
}
class Demo{
    public static void main(String args[]){
        String s1 = new String("ashish");
        String s2 = new String("ashish");
        System.out.println(s1==s2);
    }
}
```
equals() method of Object class is used to compare the reference or address of two objects i.e if two objects point to the same memory location or not

```java
class Strings extends Object{
    public boolean equals(Object obj){//this method override the method of object class and it provides its owns funcitonality as it dont check the memory address it check the content inside the object.
        //statements
    }

}
class Demo{
    public static void main(String args[]){
        String s1 = new String("ashish");
        String s2 = new String("ashish");
        System.out.println(s1.equals(s2));
    }
}

```
equals() method of String class is used for content comparison i.e it is used to check object value.

## String Class Constructor.

```java
class String{
    public String(){}
    public String(String s){}
    public String(StringBuffer sb){}
    public String(StringBuilder sb){}
    public String(char[] ch){}
    public String(byte b){}
}
```

**Example**

```java

public class StringDemo{
    public static void main(String args[]){
        String s1 = new String();//Empty constructor length of this string will be 0
        System.out.println(s1);
        String s2 = new String("abc");//2 Object 1 in heap memory and other in SCP
        System.out.println(s2);
        StringBuffer sb = new StringBuffer("Rahul");//String Buffer and String Builder create mutable string
        String s3 = new String(sb);
        System.out.println(s3);
        StringBuilder sb2 = new StringBuilder("Krishna");
        String s4 = new String(sb2);
        System.out.println(s4);
        byte[] b = {101, 102, 103, 104};//integer value will be converted into character
        String s5 = new String(b);
        System.out.println(s5);
        char[] ch = {'a','b','c','d','e','f','g','h'};
        String s6 = new String(ch);
        System.out.println(s6);
    }
}
```

**Why char array is preffered over string for storing password?**

String objects are immutable in java therefore if a password is stored as a plain text it will be availabe in memory until garabage collector clears it, but string objects literal are stored in String literal pool for re-usability and garbage collection is not applicable in SCP, which is a security threat.
With an array, you can explicitly wipe the data after you are done with it. You can overwrite the array with anything you like, and the password won't be present anywhere in the system, even before garbage collection.


## String class method.

**length()**

- The string length() method counts the number of character in the string and returns it in integer. This method return the length of any string which is equal to the number of 16 bit unicode character.If the string is null it will throw NullPointerException.

```java
class Test{
        public static void main(String args[]){
            String name = "abc";
            String email = "abc@gmail.com";
            String password = "abc123";
            System.out.print(name.length);
        }
    }
```
**isEmpty()**

- The Java String class isEmpty() method checks if the input string is empty or not. Note that here empty means the number of characters contained in a string is zero.

```java
public class IsEmptyExample{  
        public static void main(String args[]){  
            String s1="";  
            String s2="javatpoint";  
            System.out.println(s1.isEmpty());  //true
            System.out.println(s2.isEmpty());  //false
    }}  
```

**trim()**
 
- The Java String class trim() method eliminates leading and trailing spaces. The Unicode value of space character is '\u0020'. The trim() method in Java string checks this Unicode value before and after the string, if it exists then the method removes the spaces and returns the omitted string.

```java
public class StringTrimExample{  
        public static void main(String args[]){  
            String s1="  hello string   ";  
            System.out.println(s1+"javatpoint");//without trim()  - hello string   javatpoint
            System.out.println(s1.trim()+"javatpoint");//with trim()  - hello stringjavatpoint
    }}  
``` 

**equals()**

- The Java String class equals() method compares the two given strings based on the content of the string. If any character is not matched, it returns false. If all characters are matched, it returns true.

```java
 public class EqualsExample{  
        public static void main(String args[]){  
            String s1="javatpoint";  
            String s2="javatpoint";  
            String s3="JAVATPOINT";  
            String s4="python";  
            System.out.println(s1.equals(s2));//true because content and case is same  
            System.out.println(s1.equals(s3));//false because case is not same  
            System.out.println(s1.equals(s4));//false because content is not same  
    }}  
```

**equalsIgnoreCase()**

- The Java String class equalsIgnoreCase() method compares the two given strings on the basis of the content of the string irrespective of the case (lower and upper) of the string. It is just like the equals() method but doesn't check the case sensitivity. If any character is not matched, it returns false, else returns true

```java
public class EqualsIgnoreCaseExample{  
        public static void main(String args[]){  
            String s1="javatpoint";  
            String s2="javatpoint";  
            String s3="JAVATPOINT";  
            String s4="python";  
            System.out.println(s1.equalsIgnoreCase(s2));//true because content and case both are same  
            System.out.println(s1.equalsIgnoreCase(s3));//true because case is ignored  
            System.out.println(s1.equalsIgnoreCase(s4));//false because content is not same  
            }}  
```
**compareTo()**

- The Java String class compareTo() method compares the given string with the current string lexicographically. It returns a positive number, negative number, or 0.

- It compares strings on the basis of the Unicode value of each character in the strings.

- If the first string is lexicographically greater than the second string, it returns a positive number (difference of character value). If the first string is less than the second string lexicographically, it returns a negative number, and if the first string is lexicographically equal to the second string, it returns 0.

```java
public class CompareToExample{  
        public static void main(String args[]){  
            String s1="hello";  
            String s2="hello";  
            String s3="meklo";  
            String s4="hemlo";  
            String s5="flag";  
            System.out.println(s1.compareTo(s2));//0 because both are equal  
            System.out.println(s1.compareTo(s3));//-5 because "h" is 5 times lower than "m"  
            System.out.println(s1.compareTo(s4));//-1 because "l" is 1 times lower than "m"  
            System.out.println(s1.compareTo(s5));//2 because "h" is 2 times greater than "f"  
            }
            }   
```

**concat()**

- The Java String class concat() method combines specified string at the end of this string. It returns a combined string. It is like appending another string.

```java
public class ConcatExample{    
    public static void main(String args[]){    
        String s1="java string";    
        // The string s1 does not get changed, even though it is invoking the method      
        // concat(), as it is immutable. Therefore, the explicit assignment is required here.  
        s1.concat("is immutable");    
        System.out.println(s1);    //java string
        s1=s1.concat(" is immutable so assign it explicitly");    //java string is immutable so assign it explicitly
        System.out.println(s1);    
        }}    
```

**join()**

- The Java String class join() method returns a string joined with a given delimiter. In the String join() method, the delimiter is copied for each element. The join() method is included in the Java string since JDK 1.8.

**Syntax**

```
public static String join(CharSequence delimiter, CharSequence... elements)       
public static String join(CharSequence delimiter, Iterable<? extends CharSequence> elements)
```

```java
public class StringJoinExample{  
    public static void main(String args[]){  
        String joinString1=String.join("-","welcome","to","javatpoint");  
        System.out.println(joinString1);  
        }}  
```

**substring()**

- The Java String class substring() method returns a part of the string.

- We pass beginIndex and endIndex number position in the Java substring method where beginIndex is inclusive, and endIndex is exclusive. In  other words, the beginIndex starts from 0, whereas the endIndex starts from 1.

```java
public class SubstringExample{  
public static void main(String args[]){  
String s1="javatpoint";  
System.out.println(s1.substring(2,4));//returns va  
System.out.println(s1.substring(2));//returns vatpoint  
}}  
```

**replace(),replaceFirst(), replaceAll()**

```
public String replace(char oldChar, char newChar)    
public String replace(CharSequence target, CharSequence replacement)  
```

- The Java String class replace() method returns a string replacing all the old char or CharSequence to new char or CharSequence.

```
replaceFirst(String regex, String replacement)
```
- This method replaces the first occurrence of the specified regular expression (regex) in the string with the replacement.

```
public String replaceAll(String regex, String replacement)  
```
- The Java String class replaceAll() method returns a string replacing all the sequence of characters matching regex and replacement string.

```java
public class Test{
    public static void main(String args[]){
        String s1 = "This is demo";
        System.out.println(s1.replace("is","was"));//Thwas was demo
        System.out.println(s1.replaceFirst("is","was"));//Thwas is demo
        System.out.println(s1.replaceAll("is","was"));//Thwas was demo
        
    }
}
```