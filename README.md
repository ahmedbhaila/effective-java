# effective-java
Notes/Observations/Code Samples

# Chapter 2 - Creating and destroying objects

#### Consider static factory instead of constructors
Design your class to have a public static factory method. This is simply a static method that returns an instance of the class. The static factory method is not related to the factory method described in design patterns. The advantage of static factory methods over constructors is that they have names. When a class seems to require multiple constructors with same signature, replace this with static factory methods. Use a specific method name to highlight the differences. A static factory method doesnt need to construct a new instance everytime, it can choose to return a cached instance. This is similar to Flyweight pattern. Classes that follow the static factory method pattern and return a cached instance are said to be instance-controlled. We get the advantage of a class instance being a singleton or non-instantsiable. Static factory methods can return an object of any subtype of their return type. In Java 8, interfaces can have static methods.

##### Common Method Names
*from* - type conversion method that takes a parameter and returns an instance of the type. So it basically takes another type and converts into the type requested.

``` Date d = Date.from(instant) ```

*of* - Takes multiple parameters and returns an instance of the type requested

``` Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING) ```

*valueOf* - verbose version of *from* and *of*

``` Boolean.valueOf(true) ```

*instance or getInstance* - Returns an instance described by 0 or more parameters. Usually seen in singleton classes

``` SingletonClass.getInstance(options) ```

*create or newInstance* - similar to *instance* but guarantees to return a new object everytime.

``` Object newArray = Array.newInstance(classObject, arrayLen) ```



TODO: Sample code using static factory methods

#### Use a builder whenever possible
Got lots of parameters, consider using a builder. Programmers have used telescoping constructors patterns which have a constructor that has all required parameters and then more for each optional parameter so not a good idea. Another way is to use a constructor with no params and then have setters again not a good idea since it may create some inconsistent behavior that might not help when making the class immutable. Programmers would also need to add additonal mechanisms to do thread safety. So use Builder pattern (use Lombok @Builder). Builder pattern could be a problem in performance critical situations. Should only be used if there are enough parameters(4 or more).

covariant return typing -> A subclass method declared to return a subtype of the return type declared in the super-class :)
ref: Pizza example - NYPizza or Calzone. TODO

#### Singleton
A class that is instantiated exactly once. Making a class singleton can make it difficult to test. A singleton can be implemented using a private constructor and:
1. a public static final instance OR
2. a private static final instance with a public static method

With (2) you have more flexiblity to change the implementation of a singleton to something else. Special care needs to be taken for serialization. 

Another approach to creating a singleton is via the use of enum. TODO: add code. Cannot be used if you have a singleton depend on a superclass.

#### Utility Classes
Utility classes have static methods but java will add a default constructor to it by default. There is no point in creating an instance of such classes. So provide a private constructor and throw an explicit exception if someone tries to create an object using the private constructor:

``` private UtilityClass() { throw new AssertionError(); }```

#### Dependency Injection



