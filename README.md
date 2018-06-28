# effective-java
Notes/Observations/Code Samples

# Chapter 2 - Creating and destroying objects

#### Consider static factory instead of constructors
Design your class to have a public static factory method. This is simply a static method that returns an instance of the class. The static factory method is not related to the factory method described in design patterns. The advantage of static factory methods over constructors is that they have names. When a class seems to require multiple constructors with same signature, replace this with static factory methods. Use a specific method name to highlight the differences. A static factory method doesnt need to construct a new instance everytime, it can choose to return a cached instance. This is similar to Flyweight pattern. Classes that follow the static factory method pattern and return a cached instance are said to be instance-controlled. We get the advantage of a class instance being a singleton or non-instantsiable. Static factory methods can return an object of any subtype of their return type. In Java 8, interfaces can have static methods.

TODO: Sample code using static factory methods

#### Use a builder whenever possible
Got lots of parameters, consider using a builder. Programmers have used telescoping constructors patterns which have a constructor that has all required parameters and then more for each optional parameter so not a good idea. Another way is to use a constructor with no params and then have setters again not a good idea since it may create some inconsistent behavior that might not help when making the class immutable. Programmers would also need to add additonal mechanisms to do thread safety. So use Builder pattern (use Lombok @Builder)
