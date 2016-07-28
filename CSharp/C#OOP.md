
# OOPS

## TOC
* OOPS Basic
* Classes and Objects
  * Class Members
    * Properties 
	* Fields
	* Methods
	* Constructors
	* Destructors
	* Events
	* Nested Classes
	* Access Modifiers and Access Levels
	* Instantiating Classes
	* Static Classes and Members
	* Anonymous Types

* Inheritance
* Overriding Members
* Interfaces
* Generics
* Delegates
* Abstraction
* Encapsulation
* Polymorphism
* Inheritance

### OOPS Basic
* [Object Oriented Programming Concepts (OOP)](http://www.codeproject.com/Articles/22769/Introduction-to-Object-Oriented-Programming-Concep)
* [Diving in OOP](http://www.codeproject.com/Articles/771455/Diving-in-OOP-Day-Polymorphism-and-Inheritance-Ear)

### Video
* [C# Object Oriented Programming Basic to Advance](https://www.youtube.com/watch?v=e7Yj6vLyYOI)

### Class
```cs
class SampleClass
{
}
```

### Object
```cs
SampleClass sampleObject = new SampleClass();

// Set a property value.
sampleObject.sampleProperty = "Sample String";

// Call a method.
sampleObject.sampleMethod();

// Set a property value.
SampleClass sampleObject = new SampleClass{ FirstProperty = "A", SecondProperty = "B" };
```

### Class Members
####  Fields
```cs
Class SampleClass
{
    public string sampleField;
}
```

#### Properties 

```cs
class SampleClass
{
    public int SampleProperty { get; set; }
	
	private int _sample;
    public int Sample
    {
        // Return the value stored in a field.
        get { return _sample; }
        // Store the value in the field.
        set { _sample = value; }
    }
}
```

### Methods
```cs
 public int sampleMethod(string sampleParam)
    {
        // Insert code here
    }
	
public int sampleMethod(string sampleParam) {};
public int sampleMethod(int sampleParam) {}
```
	
### Constructors
```cs

public class SampleClass
{
    public SampleClass()
    {
        // Add code here
    }
}	
```

### Nested Classes
```cs
class Container
{
    class Nested
    {
        // Add code here.
    }
}

Container.Nested nestedInstance = new Container.Nested()
```

### Static Classes and Members
```cs
static class SampleClass
{
    public static string SampleString = "Sample String";
}
Console.WriteLine(SampleClass.SampleString);
```

### Anonymous Types
```cs
// sampleObject is an instance of a simple anonymous type.
var sampleObject = new { FirstProperty = "A", SecondProperty = "B" };
```	
	
## Inheritance	
### To inherit from a base class:
//By default all classes can be inherited. However, you can specify whether a class must not be used as a base class, or create a class that can be used as a base class only.
```cs
class DerivedClass:BaseClass{}
```

## Sealed Class
### Example 1
```cs
//Z inherits from Y but Z cannot override the virtual function F that is declared in X and sealed in Y.
class X
{
    protected virtual void F() { Console.WriteLine("X.F"); }
    protected virtual void F2() { Console.WriteLine("X.F2"); }
}

class Y : X
{
    sealed protected override void F() { Console.WriteLine("Y.F"); }
    protected override void F2() { Console.WriteLine("Y.F2"); }
}

class Z : Y
{
    // Attempting to override F causes compiler error CS0239.
    // protected override void F() { Console.WriteLine("C.F"); }

    // Overriding F2 is allowed.
    protected override void F2() { Console.WriteLine("Z.F2"); }
}
```

### Example 2
```cs
sealed class SealedClass
{
    public int x;
    public int y;
}

class SealedTest2
{
    static void Main()
    {
        SealedClass sc = new SealedClass();
        sc.x = 110;
        sc.y = 150;
        Console.WriteLine("x = {0}, y = {1}", sc.x, sc.y);
    }
}
// Output: x = 110, y = 150
```



//To specify that a class can be used as a base class only and cannot be instantiated:
```cs
public sealed class A { }
```

//To specify that a class can be used as a base class only and cannot be instantiated:
```cs
public abstract class B { }
```

## Abstract Class

### Example 1
```cs
interface I
{
    void M();
}
abstract class C : I
{
    public abstract void M();
}
```

### Example 2
```cs
abstract class ShapesClass
{
    abstract public int Area();
}
class Square : ShapesClass
{
    int side = 0;

    public Square(int n)
    {
        side = n;
    }
    // Area method is required to avoid
    // a compile-time error.
    public override int Area()
    {
        return side * side;
    }

    static void Main() 
    {
        Square sq = new Square(12);
        Console.WriteLine("Area of the square = {0}", sq.Area());
    }

    interface I
    {
        void M();
    }
    abstract class C : I
    {
        public abstract void M();
    }

}
// Output: Area of the square = 144
```

### Example 3
```cs
abstract class BaseClass   // Abstract class
{
    protected int _x = 100;
    protected int _y = 150;
    public abstract void AbstractMethod();   // Abstract method
    public abstract int X    { get; }
    public abstract int Y    { get; }
}

class DerivedClass : BaseClass
{
    public override void AbstractMethod()
    {
        _x++;
        _y++;
    }

    public override int X   // overriding property
    {
        get
        {
            return _x + 10;
        }
    }

    public override int Y   // overriding property
    {
        get
        {
            return _y + 10;
        }
    }

    static void Main()
    {
        DerivedClass o = new DerivedClass();
        o.AbstractMethod();
        Console.WriteLine("x = {0}, y = {1}", o.X, o.Y);
    }
}
// Output: x = 111, y = 161
```

### virtual
```cs
public virtual double Area() 
{
    return x * y;
}



class MyBaseClass
{
    // virtual auto-implemented property. Overrides can only
    // provide specialized behavior if they implement get and set accessors.
    public virtual string Name { get; set; }

    // ordinary virtual property with backing field
    private int num;
    public virtual int Number
    {
        get { return num; }
        set { num = value; }
    }
}
```

### Example 2
```cs
class TestClass
{
    public class Shape
    {
        public const double PI = Math.PI;
        protected double x, y;
        public Shape()
        {
        }
        public Shape(double x, double y)
        {
            this.x = x;
            this.y = y;
        }

        public virtual double Area()
        {
            return x * y;
        }
    }

    public class Circle : Shape
    {
        public Circle(double r) : base(r, 0)
        {
        }

        public override double Area()
        {
            return PI * x * x;
        }
    }

    class Sphere : Shape
    {
        public Sphere(double r) : base(r, 0)
        {
        }

        public override double Area()
        {
            return 4 * PI * x * x;
        }
    }

    class Cylinder : Shape
    {
        public Cylinder(double r, double h) : base(r, h)
        {
        }

        public override double Area()
        {
            return 2 * PI * x * x + 2 * PI * x * y;
        }
    }

    static void Main()
    {
        double r = 3.0, h = 5.0;
        Shape c = new Circle(r);
        Shape s = new Sphere(r);
        Shape l = new Cylinder(r, h);
        // Display results:
        Console.WriteLine("Area of Circle   = {0:F2}", c.Area());
        Console.WriteLine("Area of Sphere   = {0:F2}", s.Area());
        Console.WriteLine("Area of Cylinder = {0:F2}", l.Area());
        }
    }
    /*
        Output:
        Area of Circle   = 28.27
        Area of Sphere   = 113.10
        Area of Cylinder = 150.80
    */
```
	
### Example 1
```cs
class MyDerivedClass : MyBaseClass
{
    private string name;

   // Override auto-implemented property with ordinary property
   // to provide specialized accessor behavior.
    public override string Name
    {
        get
        {
            return name;
        }
        set
        {
            if (value != String.Empty)
            {
                name = value;
            }
            else
            {
                name = "Unknown";
            }
        }
    }

}
```

### Overriding Members


## Interfaces
An interface has the following properties:
* An interface is like an abstract base class. Any class or struct that implements the interface must implement all its members.
* An interface can't be instantiated directly. Its members are implemented by any class or struct that implements the interface.
* Interfaces can contain events, indexers, methods, and properties.
* Interfaces contain no implementation of methods.
* A class or struct can implement multiple interfaces. A class can inherit a base class and also implement one or more interfaces.



### Define an interface
```cs
interface ISampleInterface
{
    void doSomething();
}
```

```cs
//To implement an interface in a class:
class SampleClass : ISampleInterface
{
    void ISampleInterface.doSomething()
    {
        // Method implementation.
    }
}
```


#### Explicit Interface Implementation
If a class implements two interfaces that contain a member with the same signature, then implementing that member on the class will cause both interfaces to use that member as their implementation. In the following example, all the calls to Paint invoke the same method.

```cs
class Test 
{
    static void Main()
    {
        SampleClass sc = new SampleClass();
        IControl ctrl = (IControl)sc;
        ISurface srfc = (ISurface)sc;

        // The following lines all call the same method.
        sc.Paint();
        ctrl.Paint();
        srfc.Paint();
    }
}


interface IControl
{
    void Paint();
}
interface ISurface
{
    void Paint();
}
class SampleClass : IControl, ISurface
{
    // Both ISurface.Paint and IControl.Paint call this method. 
    public void Paint()
    {
        Console.WriteLine("Paint method in SampleClass");
    }
}

// Output:
// Paint method in SampleClass
// Paint method in SampleClass
// Paint method in SampleClass

```



If the two interface members do not perform the same function, however, this can lead to an incorrect implementation of one or both of the interfaces. It is possible to implement an interface member explicitly—creating a class member that is only called through the interface, and is specific to that interface. This is accomplished by naming the class member with the name of the interface and a period. For example:

```cs
public class SampleClass : IControl, ISurface
{
    void IControl.Paint()
    {
        System.Console.WriteLine("IControl.Paint");
    }
    void ISurface.Paint()
    {
        System.Console.WriteLine("ISurface.Paint");
    }
}

The class member IControl.Paint is only available through the IControl interface, and ISurface.Paint is only available through ISurface. Both method implementations are separate, and neither is available directly on the class. For example:
// Call the Paint methods from Main.

SampleClass obj = new SampleClass();
//obj.Paint();  // Compiler error.

IControl c = (IControl)obj;
c.Paint();  // Calls IControl.Paint on SampleClass.

ISurface s = (ISurface)obj;
s.Paint(); // Calls ISurface.Paint on SampleClass.

// Output:
// IControl.Paint
// ISurface.Paint

```



Explicit implementation is also used to resolve cases where two interfaces each declare different members of the same name such as a property and a method:
```cs

interface ILeft
{
    int P { get;}
}
interface IRight
{
    int P();
}
```


To implement both interfaces, a class has to use explicit implementation either for the property P, or the method P, or both, to avoid a compiler error. For example:
```cs
class Middle : ILeft, IRight
{
    public int P() { return 0; }
    int ILeft.P { get { return 0; } }
}
```

#### Explicitly Implement Interface Members
This example declares an interface, IDimensions, and a class, Box, which explicitly implements the interface members getLength and getWidth. The members are accessed through the interface instance dimensions.
```cs
interface IDimensions
{
    float getLength();
    float getWidth();
}

class Box : IDimensions
{
    float lengthInches;
    float widthInches;

    Box(float length, float width)
    {
        lengthInches = length;
        widthInches = width;
    }
    // Explicit interface member implementation: 
    float IDimensions.getLength()
    {
        return lengthInches;
    }
    // Explicit interface member implementation:
    float IDimensions.getWidth()
    {
        return widthInches;
    }

    static void Main()
    {
        // Declare a class instance box1:
        Box box1 = new Box(30.0f, 20.0f);

        // Declare an interface instance dimensions:
        IDimensions dimensions = (IDimensions)box1;

        // The following commented lines would produce compilation 
        // errors because they try to access an explicitly implemented
        // interface member from a class instance:                   
        //System.Console.WriteLine("Length: {0}", box1.getLength());
        //System.Console.WriteLine("Width: {0}", box1.getWidth());

        // Print out the dimensions of the box by calling the methods 
        // from an instance of the interface:
        System.Console.WriteLine("Length: {0}", dimensions.getLength());
        System.Console.WriteLine("Width: {0}", dimensions.getWidth());
    }
}
/* Output:
    Length: 30
    Width: 20
*/

```

#### Explicitly Implement Members of Two Interfaces
Explicit interface implementation also allows the programmer to implement two interfaces that have the same member names and give each interface member a separate implementation. This example displays the dimensions of a box in both metric and English units. The Box class implements two interfaces IEnglishDimensions and IMetricDimensions, which represent the different measurement systems. Both interfaces have identical member names, Length and Width.
```cs
// Declare the English units interface:
interface IEnglishDimensions
{
    float Length();
    float Width();
}

// Declare the metric units interface:
interface IMetricDimensions
{
    float Length();
    float Width();
}

// Declare the Box class that implements the two interfaces:
// IEnglishDimensions and IMetricDimensions:
class Box : IEnglishDimensions, IMetricDimensions
{
    float lengthInches;
    float widthInches;

    public Box(float length, float width)
    {
        lengthInches = length;
        widthInches = width;
    }

    // Explicitly implement the members of IEnglishDimensions:
    float IEnglishDimensions.Length()
    {
        return lengthInches;
    }

    float IEnglishDimensions.Width()
    {
        return widthInches;
    }

    // Explicitly implement the members of IMetricDimensions:
    float IMetricDimensions.Length()
    {
        return lengthInches * 2.54f;
    }

    float IMetricDimensions.Width()
    {
        return widthInches * 2.54f;
    }

    static void Main()
    {
        // Declare a class instance box1:
        Box box1 = new Box(30.0f, 20.0f);

        // Declare an instance of the English units interface:
        IEnglishDimensions eDimensions = (IEnglishDimensions)box1;

        // Declare an instance of the metric units interface:
        IMetricDimensions mDimensions = (IMetricDimensions)box1;

        // Print dimensions in English units:
        System.Console.WriteLine("Length(in): {0}", eDimensions.Length());
        System.Console.WriteLine("Width (in): {0}", eDimensions.Width());

        // Print dimensions in metric units:
        System.Console.WriteLine("Length(cm): {0}", mDimensions.Length());
        System.Console.WriteLine("Width (cm): {0}", mDimensions.Width());
    }
}
/* Output:
    Length(in): 30
    Width (in): 20
    Length(cm): 76.2
    Width (cm): 50.8
*/

//Robust Programming

//If you want to make the default measurements in English units, implement the methods Length and Width normally, and explicitly implement the Length and Width methods from the IMetricDimensions interface:

// Normal implementation:
public float Length()
{
    return lengthInches;
}
public float Width()
{
    return widthInches;
}

// Explicit implementation:
float IMetricDimensions.Length()
{
    return lengthInches * 2.54f;
}
float IMetricDimensions.Width()
{
    return widthInches * 2.54f;
}


//In this case, you can access the English units from the class instance and access the metric units from the interface instance:
public static void Test()
{
    Box box1 = new Box(30.0f, 20.0f);
    IMetricDimensions mDimensions = (IMetricDimensions)box1;

    System.Console.WriteLine("Length(in): {0}", box1.Length());
    System.Console.WriteLine("Width (in): {0}", box1.Width());
    System.Console.WriteLine("Length(cm): {0}", mDimensions.Length());
    System.Console.WriteLine("Width (cm): {0}", mDimensions.Width());
}
```


### override 

#### Example 1
```cs
abstract class ShapesClass
{
    abstract public int Area();
}
class Square : ShapesClass
{
    int side = 0;

    public Square(int n)
    {
        side = n;
    }
    // Area method is required to avoid
    // a compile-time error.
    public override int Area()
    {
        return side * side;
    }

    static void Main() 
    {
        Square sq = new Square(12);
        Console.WriteLine("Area of the square = {0}", sq.Area());
    }

    interface I
    {
        void M();
    }
    abstract class C : I
    {
        public abstract void M();
    }

}
// Output: Area of the square = 144
```

#### Example 2
```cs
class TestOverride
{
    public class Employee
    {
        public string name;

        // Basepay is defined as protected, so that it may be 
        // accessed only by this class and derrived classes.
        protected decimal basepay;

        // Constructor to set the name and basepay values.
        public Employee(string name, decimal basepay)
        {
            this.name = name;
            this.basepay = basepay;
        }

        // Declared virtual so it can be overridden.
        public virtual decimal CalculatePay()
        {
            return basepay;
        }
    }

    // Derive a new class from Employee.
    public class SalesEmployee : Employee
    {
        // New field that will affect the base pay.
        private decimal salesbonus;

        // The constructor calls the base-class version, and
        // initializes the salesbonus field.
        public SalesEmployee(string name, decimal basepay, 
                  decimal salesbonus) : base(name, basepay)
        {
            this.salesbonus = salesbonus;
        }

        // Override the CalculatePay method 
        // to take bonus into account.
        public override decimal CalculatePay()
        {
            return basepay + salesbonus;
        }
    }

    static void Main()
    {
        // Create some new employees.
        SalesEmployee employee1 = new SalesEmployee("Alice", 
                      1000, 500);
        Employee employee2 = new Employee("Bob", 1200);

        Console.WriteLine("Employee4 " + employee1.name + 
                  " earned: " + employee1.CalculatePay());
        Console.WriteLine("Employee4 " + employee2.name + 
                  " earned: " + employee2.CalculatePay());
    }
}
/*
    Output:
    Employee4 Alice earned: 1500
    Employee4 Bob earned: 1200
*/
```

### abstract
#### Example 1
```cs
abstract class ShapesClass
{
    abstract public int Area();
}
class Square : ShapesClass
{
    int side = 0;

    public Square(int n)
    {
        side = n;
    }
    // Area method is required to avoid
    // a compile-time error.
    public override int Area()
    {
        return side * side;
    }

    static void Main() 
    {
        Square sq = new Square(12);
        Console.WriteLine("Area of the square = {0}", sq.Area());
    }

    interface I
    {
        void M();
    }
    abstract class C : I
    {
        public abstract void M();
    }

}
// Output: Area of the square = 144
```

## New
* new Operator
* new Modifier
* new Constraint

### new Operator
```cs
//Used to create objects and invoke constructors.
Class1 obj  = new Class1();

//create struct objects and invoke constructors.
//SampleStruct Location1 = new SampleStruct();
 
//create instances of anonymous types:
var query = from cust in customers   select new {Name = cust.Name, Address = cust.PrimaryAddress};

// The new operator is also used to invoke the default constructor for value types.			
int i = new int();		

//i is initialized to 0, which is the default value for the type int. The statement has the same effect as the following:
int i = 0;	
```

### Generics
```cs
Public class SampleGeneric<T> 
{
    public T Field;
}


SampleGeneric<string> sampleObject = new SampleGeneric<string>();
sampleObject.Field = "Sample string";
```


### new Modifier
#### Example 1
```cs
public class BaseC
{
    public int x;
    public void Invoke() { }
}
public class DerivedC : BaseC
{
    new public void Invoke() { }
}
```

#### Example 2
```cs
public class BaseC
{
    public static int x = 55;
    public static int y = 22;
}

public class DerivedC : BaseC
{
    // Hide field 'x'.
    new public static int x = 100;

    static void Main()
    {
        // Display the new value of x:
        Console.WriteLine(x);

        // Display the hidden value of x:
        Console.WriteLine(BaseC.x);

        // Display the unhidden member y:
        Console.WriteLine(y);
    }
}
/*
Output:
100
55
22
*/
```

#### Example 3
```cs
public class BaseC 
{
    public class NestedC 
    {
        public int x = 200;
        public int y;
    }
}

public class DerivedC : BaseC 
{
    // Nested type hiding the base type members.
    new public class NestedC   
    {
        public int x = 100;
        public int y; 
        public int z;
    }

    static void Main() 
    {
        // Creating an object from the overlapping class:
        NestedC c1  = new NestedC();

        // Creating an object from the hidden class:
        BaseC.NestedC c2 = new BaseC.NestedC();

        Console.WriteLine(c1.x);
        Console.WriteLine(c2.x);   
    }
}
/*
Output:
100
200
*/


//If you remove the new modifier, the program will still compile and run, but you will get the following warning:
//The keyword new is required on 'MyDerivedC.x' because it hides inherited member 'MyBaseC.x'.
```

### new Constraint
#### Example1
```cs
//Apply the new constraint to a type parameter when your generic class creates new instances of the type
class ItemFactory<T> where T : new()
{
    public T GetNewItem()
    {
        return new T();
    }
}
```

#### Example1
```cs
//When you use the new() constraint with other constraints, it must be specified last:
public class ItemFactory2<T>
    where T : IComparable, new()
{
}

```

### interface 

An interface can be a member of a namespace or a class and can contain signatures of the following members:
Methods
Properties
Indexers
Events

An interface can inherit from one or more base interfaces.
When a base type list contains a base class and interfaces, the base class must come first in the list.
A class that implements an interface can explicitly implement members of that interface. An explicitly implemented member cannot be accessed through a class instance, but only through an instance of the interface.


#### Example 1

An interface contains only the signatures of methods, properties, events or indexers. A class or struct that implements the interface must implement the members of the interface that are specified in the interface definition. In the following example, class ImplementationClass must implement a method named SampleMethod that has no parameters and returns void.
```cs
interface ISampleInterface
{
    void SampleMethod();
}

class ImplementationClass : ISampleInterface
{
    // Explicit interface member implementation: 
    void ISampleInterface.SampleMethod()
    {
        // Method implementation.
    }

    static void Main()
    {
        // Declare an interface instance.
        ISampleInterface obj = new ImplementationClass();

        // Call the member.
        obj.SampleMethod();
    }
}
```

#### Example 2
The following example demonstrates interface implementation. In this example, the interface contains the property declaration and the class contains the implementation. Any instance of a class that implements IPoint has integer properties x and y.

```cs
interface IPoint
{
   // Property signatures:
   int x
   {
      get;
      set;
   }

   int y
   {
      get;
      set;
   }
}

class Point : IPoint
{
   // Fields:
   private int _x;
   private int _y;

   // Constructor:
   public Point(int x, int y)
   {
      _x = x;
      _y = y;
   }

   // Property implementation:
   public int x
   {
      get
      {
         return _x;
      }

      set
      {
         _x = value;
      }
   }

   public int y
   {
      get
      {
         return _y;
      }
      set
      {
         _y = value;
      }
   }
}

class MainClass
{
   static void PrintPoint(IPoint p)
   {
      Console.WriteLine("x={0}, y={1}", p.x, p.y);
   }

   static void Main()
   {
      Point p = new Point(2, 3);
      Console.Write("My Point: ");
      PrintPoint(p);
   }
}
// Output: My Point: x=2, y=3

```

public Cylinder(double r, double h): base(r, h) {}



# Classes

## Classes
```cs
//public, internal, abstract, sealed, static, unsafe, and partial
class YourClassName
{
}
```

## Fields
```cs
//Static modifier: static
//Access modifiers: public internal private protected
//Inheritance modifier: new
//Unsafe code modifier: unsafe
//Read-only modifier: readonly
//Threading modifier: volatile

class Octopus
{
	string name;
	public int Age = 10;
}
```

## Methods
```cs
Static modifier: static
Access modifiers: public internal private protected
Inheritance modifiers: new virtual abstract override sealed
Partial method modifier: partial
Unmanaged code modifiers: unsafe extern



//Overloading methods
void Foo (int x) {...}
void Foo (double x) {...}
void Foo (int x, float y) {...}
void Foo (float x, int y) {...}

void Foo (int x) {...}
float Foo (int x) {...} // Compile-time error
void Goo (int[] x) {...}
void Goo (params int[] x) {...} // Compile-time error


//Pass-by-value versus pass-by-reference
void Foo (int x) {...}
void Foo (ref int x) {...} // OK so far
void Foo (out int x) {...} // Compile-time error

//Partial methods
partial class PaymentForm // In auto-generated file
{
	...
	partial void ValidatePayment (decimal amount);
}	

partial class PaymentForm // In hand-authored file
{
	...
	partial void ValidatePayment (decimal amount)
	{
		if (amount > 100)
		...
	}
}
```

## Constructors
```cs
Access modifiers: public internal private protected
Unmanaged code modifiers: unsafe extern

//Overloading constructors
public class Wine
{
	public decimal Price;
	public int Year;
	public Wine (decimal price) { Price = price; }
	public Wine (decimal price, int year) : this (price) { Year = year; }
}


public class Class1
{
	Class1() {} // Private constructor
	public static Class1 Create (...)
	{
		// Perform custom logic here to return an instance of Class1
		...
	}
}
```

## Static Constructors
```cs
class Test
{
	static Test() {
		Console.WriteLine ("Type Initialized"); 
	}
}
```

## The this Reference
```cs
public class Panda
{
	public Panda Mate;
	public void Marry (Panda partner)
	{
		Mate = partner;
		partner.Mate = this;
	}
}
```

## Properties
## Properties
```cs
public class Properties
{
	public string Name{}
}
//Output
//Error 'Properties.Properties.Name': property or indexer must have at least one accessor
```

## Get accessor
```cs
public string Name
{
	get
	{
		 return "I am a Name property";
	}
}
```

```cs
public int Age
{
	get
	{
		DateTime dateOfBirth=new DateTime(1984,01,20);
		DateTime currentDate = DateTime.Now;
		int age = currentDate.Year - dateOfBirth.Year;
		return age;
	}
}
```

## Set accessor		
```cs
public int Age
{
	set
	{
		Console.WriteLine("Set Age called " + value);
	}
}	
```

### Auto
```cs
public string Name { get; set; }
public int Age { get;  }
public int Age {  set; }
```

### Readonly
```cs
public int Age { get { return age; } }
```

### Write-Only
```cs
public int Age { set { age = value; } }
```

### Static Properties
```cs
public static int Age
{
	set
	{
		Console.WriteLine("In set static property; value is " + value);
	}
	get
	{
		Console.WriteLine("In get static property");
		return 10;
	}
}
```

### Abstract Propertiesnamespace Properties
```cs

    public abstract class BaseClass
    {
        public abstract int AbsProperty { get; set; }
    }

    public class Properties : BaseClass
    {
        public override int AbsProperty
        {
            get
            {
                return 10;
            }
            set { Console.WriteLine("set called,value is " + value); }
        }
    }

```

### Properties in Inheritance
```cs
namespace Properties
{
  public class PropertiesBaseClass 
    {
        public int Age
        {
            set {}
        }
    }

    public class PropertiesDerivedClass:PropertiesBaseClass
    {
        public int Age
        {
            get { return 32; }
        }
    }
}

namespace Properties
{
    class Program
    {
        static void Main(string[] args)
        {
            PropertiesBaseClass pBaseClass=new PropertiesBaseClass();
            pBaseClass.Age = 10;
            PropertiesDerivedClass pDerivedClass=new PropertiesDerivedClass();
            ((PropertiesBaseClass) pDerivedClass).Age = 15;
            pDerivedClass.Age = 10;
        }
    }
}
```




### CLR property implementation
```cs
public decimal get_CurrentPrice {...}
public void set_CurrentPrice (decimal value) {...}
```
## Indexers


## Index
```cs
static void Main(string[] args)
{
	Indexer indexer=new Indexer();
	indexer[1] = 50;
}
//Output
Compile the code. Error Cannot apply indexing with [] to an expression of type 'Indexers.Indexer'
```

```cs
namespace Indexers
{
    public class Indexer
    {
		public int this[int indexValue]
        {
            set
            {
                Console.WriteLine("I am in set : Value is " + value + " and indexValue is " + indexValue);
            }
             get
            {
                Console.WriteLine("I am in get and indexValue is " + indexValue);
                return 30;
            }
        }
    }
	
	class Program
    {
        static void Main(string[] args)
        {
            Indexer indexer=new Indexer();
            indexer["name"]=20;
            Console.WriteLine(indexer["name"]);
        }
    }
	
}
```
		
		
### Indexers in interfaces
```cs
namespace Indexers
{
    interface IIndexers
    {
        string this[int indexerValue] { get; set; }
    }

    public class IndexerClass:IIndexers
    {
        readonly string[] _nameList = { "AKhil","Bob","Shawn","Sandra" };

        public string this[int indexerValue]
        {
            get
            {
                return _nameList[indexerValue];
            }
            set
            {
                _nameList[indexerValue] = value;
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
           IIndexers iIndexer=new IndexerClass();
            Console.WriteLine(iIndexer[0]);
            Console.WriteLine(iIndexer[1]);
            Console.WriteLine(iIndexer[2]);
            Console.WriteLine(iIndexer[3]);
            Console.ReadLine();

        }
    }
}
```

### Indexers in Abstract class
```cs
namespace Indexers
{
	//AbstractBaseClass
    public abstract class AbstractBaseClass
    {
        public abstract string this[int indexerValue] { get; set; }
    }

	//IndexerClass
    public class IndexerClass:AbstractBaseClass
    {
        readonly string[] _nameList = { "AKhil","Bob","Shawn","Sandra" };

        public override string this[int indexerValue]
        {
            get
            {
                return _nameList[indexerValue];
            }
            set
            {
                _nameList[indexerValue] = value;
            }
        }
    }
}

//Program.cs
class Program
{
	static void Main(string[] args)
	{
	   AbstractBaseClass absIndexer=new IndexerClass();
		Console.WriteLine(absIndexer[0]);
		Console.WriteLine(absIndexer[1]);
		Console.WriteLine(absIndexer[2]);
		Console.WriteLine(absIndexer[3]);
		absIndexer[2] = "Akhil Mittal";
		Console.WriteLine(absIndexer[2]);

		Console.ReadLine();

	}
}
```

### Indexer Overloading
```cs
public class Indexer
{
	public int this[int indexerValue]
	{
		set
		{
			Console.WriteLine("Integer value " + indexerValue + " " + value);
		}
	}

	public int this[string indexerValue]
	{
		set
		{
			Console.WriteLine("String value " + indexerValue + " " + value);
		}
	}

	public int this[string indexerValue, int indexerintValue]
	{
		set
		{
			Console.WriteLine("String and integer value " + indexerValue + " " + indexerintValue + " " + value);
		}
	}
}
	
class Program
{
	static void Main(string[] args)
	{
		Indexer indexer=new Indexer();
		indexer[1] = 30;
		indexer["name"]=20;
		indexer["address",2] = 40;
		Console.ReadLine();
	}
}
```

### Inheritance/Polymorphism in Indexers
```cs
//Indexer.cs
namespace Indexers
{
    public class IndexerBaseClass
    {
        public virtual int this[int indexerValue]
        {
            get
            {
                Console.WriteLine("Get of IndexerBaseClass; indexer value: " + indexerValue);
                return 100;
            }
            set
            {
                Console.WriteLine("Set of IndexerBaseClass; indexer value: " + indexerValue + " set value " + value);
            }

        }
    }
    public class IndexerDerivedClass:IndexerBaseClass
    {
        public override int this[int indexerValue]
        {
            get
            {
                int dValue = base[indexerValue];
                Console.WriteLine("Get of IndexerDerivedClass; indexer value: " + indexerValue + " dValue from base class indexer: " + dValue);
                return 500;
            }
            set
            {
                Console.WriteLine("Set of IndexerDerivedClass; indexer value: " + indexerValue + " set value " + value);
                base[indexerValue] = value;
            }

        }
    }
}

//Program.cs
class Program
{
	static void Main(string[] args)
	{
		IndexerDerivedClass indexDerived=new IndexerDerivedClass();
		indexDerived[2] = 300;
		Console.WriteLine(indexDerived[2]);
		Console.ReadLine();

	}
}
```	

### Implementing an indexer
```cs
class Sentence
{
	string[] words = "The quick brown fox".Split();
	
	public string this [int wordNum] // indexer
	{
		get { return words [wordNum]; }
		set { words [wordNum] = value; }
	}
}

Sentence s = new Sentence();
Console.WriteLine (s[3]); // fox
s[3] = "kangaroo";
Console.WriteLine (s[3]); // kangaroo
```

### Constants
```cs
public class Test
{
	public const string Message = "Hello World";
}
```
### Finalizers
```cs
class Class1
{
	~Class1()
	{
		...
	}
}

//This is actually C# syntax for overriding Object’s Finalize method, 
//and the compiler expands it into the following method declaration:
protected override void Finalize()
{
	...
	base.Finalize();
}
```


## Abstract Classes

### Abstract Classes in Action
* We cannot create an object of abstract class using new keyword. 
* Seems that the class is useless for us as we cannot use it for other practical purposes as we used to do.

```cs
namespace InheritanceAndPolymorphism
{
    public abstract class ClassA
    {  }

    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA classA = new ClassA();
        }
    }
}

//Output
//Compile time error: Cannot create an instance of the abstract class or interface 'InheritanceAndPolymorphism.ClassA'
```

### Non Abstract Method Definition in Abstract Class
```cs
public abstract class ClassA
{
	//add some code to our abstract class:
    public int a;
    public void XXX()
    {    }
}

public class Program
{
    private static void Main(string[] args)
    {
		//we cannot use new if we have already used an abstract modifier.
        ClassA classA = new ClassA();
        Console.ReadKey();
    }
}
Output
Compile time error: Cannot create an instance of the abstract class or interface 'InheritanceAndPolymorphism.ClassA'
```

### Abstract Class Acting as a Base Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }
}

public class ClassB:ClassA
{
}

public class Program
{
    private static void Main(string[] args)
    {
		// A class can be derived from abstract class. 
		// Creating an object of ClassB does not gives us any error.
        ClassB classB = new ClassB();
    }
}
```

### Non Abstract Method Declaration in Abstract Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {

    }

    public void YYY();
}

//A class can be derived from an abstract class.
public class ClassB:ClassA
{

}

public class Program
{
    private static void Main(string[] args)
    {
		//A object of a class derived from an abstract class can be created using new.
        ClassB classB = new ClassB();
        Console.ReadKey();
    }
}

//Output
//Compile time error: 'InheritanceAndPolymorphism.ClassA.YYY()' must declare a body because it is not marked abstract, extern, or partial
```

###  Abstract Method Declaration in Abstract Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Compiler error: 'InheritanceAndPolymorphism.ClassB' does not implement  inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
```

### Abstract Method Implementation in Derived Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}


public class ClassB:ClassA
{
    public void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Compile time error: 'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
Compile time warning: 'InheritanceAndPolymorphism.ClassB.YYY()' hides inherited member 'InheritanceAndPolymorphism.ClassA.YYY()'.
```


### Abstract Method Declaration in Abstract Class
```cs
public abstract class ClassA
{
	public int a;
	public void XXX()
	{
	}

	abstract public void YYY();
}


public class ClassB:ClassA
{
	//If any method as abstract in our abstract class, then derived class must  provide the body for that abstract method
	//unless a body is provided for that abstract method, we cannot create an object of that derived class.
	public override void YYY()
	{
	}
}

public class Program
{
	private static void Main(string[] args)
	{
		ClassB classB = new ClassB();
	}
}
Output
Compiler error: 'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
```	
	
### Abstract Method Implementation in Derived Class
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
    public void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Two compile time errors this time:
Compile time error: 'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY()'
Compile time warning: 'InheritanceAndPolymorphism.ClassB.YYY()' hides inherited member 'InheritanceAndPolymorphism.ClassA.YYY()'.

```

```cs
To make a member override that implementation, add the override keyword.
public abstract class ClassA
{
	public int a;
	public void XXX()
	{
	}

   abstract public void YYY();
}

public class ClassB:ClassA
{
	public override void YYY()
	{
	}
}

public class Program
{
	private static void Main(string[] args)
	{
		ClassB classB = new ClassB();
	}
}
```
	
	
### Abstract Method Implementation in Derived Class with Different Return Type
```cs
public abstract class ClassA
{
  public int a;
  public void XXX()
  {
  }

 abstract public void YYY();
}

public class ClassB:ClassA
{
  public override int YYY()
  {
  }
}


public class Program
{
  private static void Main(string[] args)
  {
	  ClassB classB = new ClassB();
  }
}
 
Output
Compile time error: 'InheritanceAndPolymorphism.ClassB.YYY()': return type must be 'void' to match overridden member 'InheritanceAndPolymorphism.ClassA.YYY()'
```
	

```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
   abstract public void YYY1();
   abstract public void YYY2();
   abstract public void YYY3();
}

public class ClassB:ClassA
{
    public override void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Compiler error:
'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY3()'
'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY2()'
'InheritanceAndPolymorphism.ClassB' does not implement inherited abstract member 'InheritanceAndPolymorphism.ClassA.YYY1()'
```
	
### Abstract Method in Non Abstract Class
```cs
public class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
    public override void YYY()
    {
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}

Output
Compiler error: 'InheritanceAndPolymorphism.ClassA.YYY()' is abstract but it is contained in non-abstract class 'InheritanceAndPolymorphism.ClassA'
```

### Abstract Base Method
```cs
public abstract class ClassA
{
    public int a;
    public void XXX()
    {
    }

   abstract public void YYY();
}

public class ClassB:ClassA
{
    public override void YYY()
    {
         base.YYY();
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassB classB = new ClassB();
    }
}
Output
Compile time error : Cannot call an abstract base member: 'InheritanceAndPolymorphism.ClassA.YYY()'
```

### Abstract Class Acting as Derived as Well as Base Class
```cs
public class ClassA
{
    public virtual void XXX()
    {
        Console.WriteLine("ClassA XXX");
    }
}

public abstract class ClassB:ClassA
{
    public new abstract void XXX();
}

public class ClassC:ClassB
{
    public override void XXX()
    {
        System.Console.WriteLine("ClassC XXX");
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassA classA = new ClassC();
        ClassB classB = new ClassC();
        classA.XXX(); classB.XXX();
    }
}	
Output
ClassA XXX
ClassC XXX
```


### Can Abstract Class be Sealed?
* Abstract class cannot be sealed class.
* Abstract class cannot be a static class.
```cs
public sealed abstract class ClassA
{
    public abstract void XXX()
    {
        Console.WriteLine("ClassA XXX");
    }
}

public class Program
{
    private static void Main(string[] args)
    {
    }
}

Output
Compile time error: 'InheritanceAndPolymorphism.ClassA': an abstract class cannot be sealed or static 
```


## Polymorphism

### Method Overloading or Early Binding or Compile Time Polymorphism
*  C# recognizes the method by its parameters and not only by its name.
```cs
public class Overload
{
  public void DisplayOverload(int a){
	  System.Console.WriteLine("DisplayOverload " + a);
  }
  public void DisplayOverload(string a){
	  System.Console.WriteLine("DisplayOverload " + a);
  }
  public void DisplayOverload(string a, int b){
	  System.Console.WriteLine("DisplayOverload " + a + b);
  }
}
```


```cs
public void DisplayOverload() { }
public int DisplayOverload(){ }

Output
Error: Type 'InheritanceAndPolymorphism.Overload' already defines a member called 'DisplayOverload' with the same parameter types

Point to remember: The return value/parameter type of a method is never the part of method signature if the names of the methods are same. So this is not polymorphism.
Point to remember: Modifiers such as static are not considered as part of method signature.
```

## xx
```cs
private void DisplayOverload(int a) {   }

private void DisplayOverload(out int a)
{
	a = 100;
}

private void DisplayOverload(ref int a) {   }

Output
Error: Cannot define overloaded method 'DisplayOverload' because it differs from another method only on ref and out
```

## Role of Params Parameter in Polymorphism
```cs
//Point to remember: Parameter names should be unique. And also we can not have a parameter name and a declared variable name in the same function as same.

public void DisplayOverload(int a, string a)  {   }

public void Display(int a)
{
	string a;
}

Error1: The parameter name 'a' is a duplicate
Error2: A local variable named 'a' cannot be declared in this scope because it would give a different meaning to 'a', which is already used in a 'parent or current' scope to denote something else

```

```cs
public class Overload
{
	public void Display()
	{
		DisplayOverload(100, "Akhil", "Mittal", "OOP");
		DisplayOverload(200, "Akhil");
		DisplayOverload(300);
	}

	private void DisplayOverload(int a, params string[] parameterArray)
	{
		foreach (string str in parameterArray)
		   Console.WriteLine(str + " " + a);
	}
}

class Program
{
	static void Main(string[] args)
	{
		Overload overload = new Overload();
		overload.Display();
		Console.ReadKey();
	}
}
Error: A parameter array must be the last parameter in a formal parameter list	
```

## 
```cs
Point to Remember: C# is very smart to recognize if the penultimate argument and the params have the same data type.
public class Overload
{
    public void Display()
    {
        DisplayOverload(100, 200, 300);
        DisplayOverload(200, 100);
        DisplayOverload(200);
    }

    private void DisplayOverload(int a, params int[] parameterArray)
    {
        foreach (var i in parameterArray)
            Console.WriteLine(i + " " + a);
    }

}

class Program
{
	static void Main(string[] args)
	{
		Overload overload = new Overload();
		overload.Display();
		Console.ReadKey();
	}
}
Error: The parameter array must be a single dimensional array	
```


```cs
public class Overload
    {
        public void Display()
        {
            string[] names = {"Akhil", "Ekta", "Arsh"};
            DisplayOverload(3, names);
        }

        private void DisplayOverload(int a, params string[] parameterArray)
        {
            foreach (var s in parameterArray)
                Console.WriteLine(s + " " + a);
        }

    }
```

```cs
public class Overload
{
	public void Display()
	{
	   string [] names = {"Akhil","Arsh"};
	   DisplayOverload(2, names, "Ekta");
	}

	private void DisplayOverload(int a, params string[] parameterArray)
	{
		foreach (var str in parameterArray)
			Console.WriteLine(str + " " + a);
	}

}
Output
Error: The best overloaded method match for 'InheritanceAndPolymorphism.Overload.DisplayOverload(int, params string[])' has some invalid arguments
Error:Argument 2: cannot convert from 'string[]' to 'string'

```


```cs
public class Overload
{
	public void Display()
	{
		int[] numbers = {10, 20, 30};
		DisplayOverload(40, numbers);
		Console.WriteLine(numbers[1]);
	}

	private void DisplayOverload(int a, params int[] parameterArray)
	{
		parameterArray[1] = 1000;
	}

}
Output
1000
```

```cs
public class Overload
{
	public void Display()
	{
		int number = 102;
		DisplayOverload(200, 1000, number, 200);
		Console.WriteLine(number);
	}

	private void DisplayOverload(int a, params int[] parameterArray)
	{
		parameterArray[1] = 3000;
	}

}
Output
102
```

```cs
public class Overload
{
	public void Display()
	{
		DisplayOverload(200);
		DisplayOverload(200, 300);
		DisplayOverload(200, 300, 500, 600);
	}

	private void DisplayOverload(int x, int y)
	{
		Console.WriteLine("The two integers " + x + " " + y);
	}

	private void DisplayOverload(params int[] parameterArray)
	{
		Console.WriteLine("parameterArray");
	}

}

Output
parameterArray
The two integers 200 300
parameterArray
```

```cs
public class Overload
{
	public static void Display(params object[] objectParamArray)
	{
		foreach (object obj in objectParamArray)
		{
			Console.Write(obj.GetType().FullName + " ");
		}
		Console.WriteLine();

	}
}

class Program
{
	static void Main(string[] args)
	{
		object[] objArray = { 100, "Akhil", 200.300 };
		object obj = objArray;
		Overload.Display(objArray);
		Overload.Display((object)objArray);
		Overload.Display(obj);
		Overload.Display((object[])obj);
		Console.ReadKey();

	}
}

Output
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
	
```

## Inheritance


```cs
class ClassA
 {
	
 }

class ClassB
{
	public int x = 100;
	public void Display1()
	{
		Console.WriteLine("ClassB Display1");
	}
	public void Display2()
	{
		Console.WriteLine("ClassB Display2");
	}
}

class Program
  {
      static void Main(string[] args)
      {

          ClassA a = new ClassA();
          a.Display1();
      }
  }
Output:
Error: 'InheritanceAndPolymorphism.ClassA' does not contain a definition for 'Display1' and no extension method 'Display1' accepting a first argument of type 'InheritanceAndPolymorphism.ClassA' could be found (are you missing a using directive or an assembly reference?)
  
```

```cs
class ClassA:ClassB
{
}

class ClassB
{
	public int x = 100;
	public void Display1()
	{
		Console.WriteLine("ClassB Display1");
	}
	public void Display2()
	{
		Console.WriteLine("ClassB Display2");
	}
}
	
class Program
{
	static void Main(string[] args)
	{
		ClassA a = new ClassA();
		a.Display1();
		Console.ReadKey();
	}
}
	
Output
ClassB Display1
```

```cs
class ClassA:ClassB
    {
		//No one can stop a derived class to have a method with the same name already declared in its base class.
        public void Display1()
        {
            System.Console.WriteLine("ClassA Display1");
        }
    }

class ClassB
    {
        public int x = 100;
        public void Display1()
        {
            Console.WriteLine("ClassB Display1");
        }
        public void Display2()
        {
            Console.WriteLine("ClassB Display2");
        }
    
	class Program
    {
        static void Main(string[] args)
        {
            ClassA a = new ClassA();
            a.Display1();
            Console.ReadKey();
        }
    }
Output:
ClassA Display1
Warning: 'InheritanceAndPolymorphism.ClassA.Display1()' hides inherited member 'InheritanceAndPolymorphism.ClassB.Display1()'. Use the new keyword if hiding was intended.
	
```

```cs
ClassA:

  class ClassA:ClassB
    {
        public void Display1()
        {
            Console.WriteLine("ClassA Display1");
            base.Display1();
        }
    }

ClassB:

class ClassB
    {
        public int x = 100;
        public void Display1()
        {
            Console.WriteLine("ClassB Display1");
        }
        public void Display2()
        {
            Console.WriteLine("ClassB Display2");
        }
    }
class Program
    {
        static void Main(string[] args)
        {
            ClassA a = new ClassA();
            a.Display1();
            Console.ReadKey();
        }
    }	
	
	Output
	ClassA Display1 
ClassB Display1
```

```cs
/// <summary>
/// ClassB: acting as base class
/// </summary>
class ClassB
 {
     public int x = 100;
     public void Display1()
     {
         Console.WriteLine("ClassB Display1");
     }
     public void Display2()
     {
         Console.WriteLine("ClassB Display2");
     }
 }

 /// <summary>
 /// ClassA: acting as derived class
 /// </summary>
 class ClassA : ClassB
 {
     public void Display1()
     {
         Console.WriteLine("ClassA Display1");
         base.Display2();
     }
 }

 /// <summary>
 /// Program: used to execute the method.
 /// Contains Main method.
 /// </summary>
 class Program
 {
     static void Main(string[] args)
     {
         ClassA a = new ClassA();
         a.Display1();
         Console.ReadKey();
     }
 }
 Output
 ClassA Display1
ClassB Display2
```

```cs
/// <summary>
/// ClassB: acting as base class
/// </summary>
class ClassB
 {
     public int x = 100;
     public void Display1()
     {
         Console.WriteLine("ClassB Display1");
     }
 }

 /// <summary>
 /// ClassA: acting as derived class
 /// </summary>
 class ClassA : ClassB
 {
     public void Display2()
     {
         Console.WriteLine("ClassA Display2");
     }
 }

 /// <summary>
 /// Program: used to execute the method.
 /// Contains Main method.
 /// </summary>
 class Program
 {
     static void Main(string[] args)
     {
         ClassB b = new ClassB();
         b.Display2();
         Console.ReadKey();
     }
 }
 
 Output

Error: 'InheritanceAndPolymorphism.ClassB' does not contain a definition for 'Display2' and no extension method 'Display2' accepting a first argument of type 'InheritanceAndPolymorphism.ClassB' could be found (are you missing a using directive or an assembly reference?)
Point to remember: Inheritance does not work backwards.
Point to remember: Except constructors and destructors, a class inherits everything from its base class .

```

```cs
 classes defined cannot inherit from special built in classes in C#.
public class ClassW : System.ValueType
  {
  }

  public class ClassX : System.Enum
  {
  }

  public class ClassY : System.Delegate
  {
  }

  public class ClassZ : System.Array
  {
  }
  
  Errors
  'InheritanceAndPolymorphism.ClassW' cannot derive from special class 'System.ValueType'
'InheritanceAndPolymorphism.ClassX' cannot derive from special class 'System.Enum'
'InheritanceAndPolymorphism.ClassY' cannot derive from special class 'System.Delegate'
'InheritanceAndPolymorphism.ClassZ' cannot derive from special class 'System.Array'
  In inheritance in C#, custom classes cannot derive from special built in c# classes like System.ValueType, System.Enum, System.Delegate, System.Array, etc.
```

```cs
public class ClassW
  {
  }

  public class ClassX
  {
  }

  public class ClassY : ClassW, ClassX
  {
  }
  
  Compile time Error: Class 'InheritanceAndPolymorphism.ClassY' cannot have multiple base classes: 'InheritanceAndPolymorphism.ClassW' and 'ClassX'.
  
  So one more Point to remember: A class can only be derived from one class in C#. C# does not support multiple inheritance by means of class*.
  
  *Multiple inheritance in C# can be accomplished by the use of Interfaces
  
```

```cs
//Circular dependency is not allowed in inheritance in C#.
public class ClassW:ClassY
 {
 }

 public class ClassX:ClassW
 {
 }

 public class ClassY :  ClassX
 {
 }
 Error: Circular base class dependency involving 'InheritanceAndPolymorphism.ClassX' and 'InheritanceAndPolymorphism.ClassW'.
 ```
 
```cs
Point to remember:  We can equate an object of a base class to a derived class but not vice versa.
public class ClassB
 {
     public int b = 100;
 }

 public class ClassA:ClassB
 {
     public int a = 100;
 }

 public class Program
 {
     private static void Main(string[] args)
     {
         ClassB classB = new ClassB();
         ClassA classA = new ClassA();
         classA = classB;
         classB = classA;
     }
 }
 Error: Cannot implicitly convert type 'InheritanceAndPolymorphism.ClassB' to 'InheritanceAndPolymorphism.ClassA'. An explicit conversion exists (are you missing a cast?)
 Point to remember:  We can equate an object of a base class to a derived class but not vice versa.
 ```
 
 ```cs
 public class ClassB
    {
        public int b = 100;
    }

    public class ClassA:ClassB
    {
        public int a = 100;
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassB classB = new ClassB();
            ClassA classA = new ClassA();
            classB=classA;
            classA = (ClassA)classB;
        }
    }
	
 ```
  ```cs
  public class ClassB
 {
     public int b = 100;
 }

 public class ClassA // Removed ClassB as base class
 {
     public int a = 100;
 }

 /// <summary>
 /// Program: used to execute the method.
 /// Contains Main method.
 /// </summary>
 public class Program
 {
     private static void Main(string[] args)
     {
         ClassB classB = new ClassB();
         ClassA classA = new ClassA();
         classB = (ClassB)classA;
         classA = (ClassA)classB;
     }
 }
 Output
 Cannot convert type 'InheritanceAndPolymorphism.ClassA' to 'InheritanceAndPolymorphism.ClassB'
Cannot convert type 'InheritanceAndPolymorphism.ClassB' to 'InheritanceAndPolymorphism.ClassA' 
 ```
  ```cs
  /// <summary>
/// Program: used to execute the method.
/// Contains Main method.
/// </summary>
public class Program
{
    private static void Main(string[] args)
    {
        int integerA = 10;
        char characterB = 'A';
        integerA = characterB;
        characterB = integerA;
    }
}
Output

Error: Cannot implicitly convert type 'int' to 'char'. An explicit conversion exists (are you missing a cast?)

Point to remember: We cannot implicitly convert an int to char, but char can be converted to int.
 ```

 
##Dynamic Binding/Run Time Polymorphism
```cs
/// <summary>
/// ClassB, acting as a base class
/// </summary>
public class ClassB
{
    public void AAA()
    {
        Console.WriteLine("ClassB AAA");
    }

    public void BBB()
    {
        Console.WriteLine("ClassB BBB");
    }

    public void CCC()
    {
        Console.WriteLine("ClassB CCC");
    }
}

public class ClassA : ClassB
{
    public void AAA()
    {
        Console.WriteLine("ClassA AAA");
    }

    public void BBB()
    {
        Console.WriteLine("ClassA BBB");
    }

    public void CCC()
    {
        Console.WriteLine("ClassA CCC");
    }
}

public class Program
{
    private static void Main(string[] args)
    {
        ClassA x = new ClassA();
        ClassB y=new ClassB();
        ClassB z=new ClassA();

        x.AAA(); x.BBB(); x.CCC();
        y.AAA(); y.BBB();y.CCC();
        z.AAA(); z.BBB(); z.CCC();
    }
}
Output
ClassA AAA
ClassA BBB
ClassA CCC
ClassB AAA
ClassB BBB
ClassB CCC
ClassB AAA
ClassB BBB
ClassB CCC
'InheritanceAndPolymorphism.ClassA.AAA()' hides inherited member 'InheritanceAndPolymorphism.ClassB.AAA()'. Use the new keyword if hiding was intended.
'InheritanceAndPolymorphism.ClassA.BBB()' hides inherited member 'InheritanceAndPolymorphism.ClassB.BBB()'. Use the new keyword if hiding was intended.
'InheritanceAndPolymorphism.ClassA.CCC()' hides inherited member 'InheritanceAndPolymorphism.ClassB.CCC()'. Use the new keyword if hiding was intended.
```

```cs


/// <summary>
    /// ClassB, acting as a base class
    /// </summary>
    public class ClassB
    {
        public virtual void AAA()
        {
            Console.WriteLine("ClassB AAA");
        }

        public virtual void BBB()
        {
            Console.WriteLine("ClassB BBB");
        }

        public virtual void CCC()
        {
            Console.WriteLine("ClassB CCC");
        }
    }

    /// <summary>
    /// Class A, acting as a derived class
    /// </summary>
    public class ClassA : ClassB
    {
        public override void AAA()
        {
            Console.WriteLine("ClassA AAA");
        }

        public new void BBB()
        {
            Console.WriteLine("ClassA BBB");
        }

        public void CCC()
        {
            Console.WriteLine("ClassA CCC");
        }
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassB y = new ClassB();
            ClassA x = new ClassA();
            ClassB z = new ClassA();

            y.AAA(); y.BBB(); y.CCC();
            x.AAA(); x.BBB(); x.CCC();
            z.AAA(); z.BBB(); z.CCC();

            Console.ReadKey();
        }
    }
```

### Run Time Polymorphism with Three Classes
```cs
/// <summary>
/// ClassB, acting as a base class
/// </summary>
public class ClassB
{
    public  void AAA()
    {
        Console.WriteLine("ClassB AAA");
    }

    public virtual void BBB()
    {
        Console.WriteLine("ClassB BBB");
    }

    public virtual void CCC()
    {
        Console.WriteLine("ClassB CCC");
    }
}

/// <summary>
/// Class A, acting as a derived class
/// </summary>
public class ClassA : ClassB
{
    public virtual void AAA()
    {
        Console.WriteLine("ClassA AAA");
    }

    public new void BBB()
    {
        Console.WriteLine("ClassA BBB");
    }

    public override void CCC()
    {
        Console.WriteLine("ClassA CCC");
    }
}

/// <summary>
/// Class C, acting as a derived class
/// </summary>
public class ClassC : ClassA
{
    public override void AAA()
    {
        Console.WriteLine("ClassC AAA");
    }

    public void CCC()
    {
        Console.WriteLine("ClassC CCC");
    }
}

/// <summary>
/// Program: used to execute the method.
/// Contains Main method.
/// </summary>
public class Program
{
    private static void Main(string[] args)
    {
        ClassB y = new ClassA();
        ClassB x = new ClassC();
        ClassA z = new ClassC();

        y.AAA(); y.BBB(); y.CCC();
        x.AAA(); x.BBB(); x.CCC();
        z.AAA(); z.BBB(); z.CCC();

        Console.ReadKey();
    }
}
Output
ClassB AAA
ClassB BBB
ClassA CCC
ClassB AAA
ClassB BBB
ClassA CCC
ClassC AAA
ClassA BBB
ClassA CCC

Point to remember: If the base class object declared the method virtual and the derived class used the modifier override, the derived class method will get called. Otherwise the base class method will get executed. Therefore for virtual methods, the data type created is decided at run time only.

Point to remember: All the methods not marked with virtual are non virtual, and the method to be called is decided at compile time, depending upon the static data type of the object.

```

```cs
internal class A
{
    public virtual void X()
    {
    }
}

internal class B : A
{
    public new void X()
    {
    }
}

internal class C : B
{
    public override void X()
    {
    }
}

Error: 'InheritanceAndPolymorphism.C.X()': cannot override inherited member 
'InheritanceAndPolymorphism.B.X()' because it is not marked virtual, abstract, or override

```

### Cut Off Relations
```cs
internal class A
{
    public virtual void X()
    {
        Console.WriteLine("Class: A ; Method X");
    }
}

internal class B : A
{
    public new virtual void X()
    {
        Console.WriteLine("Class: B ; Method X");
    }
}

internal class C : B
{
    public override void X()
    {
        Console.WriteLine("Class: C ; Method X");
    }
}

/// <summary>
/// Program: used to execute the method.
/// Contains Main method.
/// </summary>
public class Program
{
    private static void Main(string[] args)
    {
        A a = new C();
        a.X();
        B b = new C();
        b.X();

        Console.ReadKey();
    }
}
Output

Hide   Copy Code
Class: A ; Method X
Class: C ; Method X
If in the above code, we remove the modifier override from X() in class C, we get:

Output

Hide   Copy Code
Class: A ; Method X
Class: B ; Method X

```

### Runtime Polymorphism with Four Classes
```cs
/// <summary>
    /// Class A
    /// </summary>
    public class ClassA
    {
        public virtual void XXX()
        {
            Console.WriteLine("ClassA XXX");
        }
    }

    /// <summary>
    /// ClassB
    /// </summary>
    public class ClassB:ClassA 
    {
        public override void XXX()
        {
            Console.WriteLine("ClassB XXX");
        }
    }

    /// <summary>
    /// Class C
    /// </summary>
    public class ClassC : ClassB
    {
        public virtual new void XXX()
        {
            Console.WriteLine("ClassC XXX");
        }
    }

    /// <summary>
    /// Class D
    /// </summary>
    public class ClassD : ClassC
    {
        public override void XXX()
        {
            Console.WriteLine("ClassD XXX");
        }
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA a = new ClassD();
            ClassB b = new ClassD();
            ClassC c=new ClassD();
            ClassD d=new ClassD();
           
            a.XXX();
            b.XXX();
            c.XXX();
            d.XXX();

            Console.ReadKey();
        }
    }
	
	Output
	ClassB XXX
ClassB XXX
ClassD XXX
ClassD XXX
```

```cs
/// <summary>
    /// Class A
    /// </summary>
    public class ClassA
    {
        public virtual void XXX()
        {
            Console.WriteLine("ClassA XXX");
        }
    }

    /// <summary>
    /// ClassB
    /// </summary>
    public class ClassB:ClassA 
    {
        public override void XXX()
        {
            base.XXX();
            Console.WriteLine("ClassB XXX");
        }
    }

    /// <summary>
    /// Class C
    /// </summary>
    public class ClassC : ClassB
    {
        public override void XXX()
        {
            base.XXX();
            Console.WriteLine("ClassC XXX");
        }
    }

    /// <summary>
    /// Class D
    /// </summary>
    public class ClassD : ClassC
    {
        public override void XXX()
        {
            Console.WriteLine("ClassD XXX");
        }
    }

    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA a = new ClassB();
            a.XXX();
            ClassB b = new ClassC();
            b.XXX();
            Console.ReadKey();
        }
    }
	
	Output

Hide   Copy Code
ClassA XXX
ClassB XXX
ClassA XXX
ClassB XXX
ClassC XXX

```
### The Infinite Loop
```cs
/// <summary>
    /// Class A
    /// </summary>
    public class ClassA
    {
        public virtual void XXX()
        {
            Console.WriteLine("ClassA XXX");
        }
    }

    /// <summary>
    /// ClassB
    /// </summary>
    public class ClassB:ClassA 
    {
        public override void XXX()
        {
            ((ClassA)this).XXX();
            Console.WriteLine("ClassB XXX");
        }
    }

   
    /// <summary>
    /// Program: used to execute the method.
    /// Contains Main method.
    /// </summary>
    public class Program
    {
        private static void Main(string[] args)
        {
            ClassA a = new ClassB();
            a.XXX();
           
        }
    }
```


# Inheritance
```cs
public class Asset
{
	public string Name;
}

public class Stock : Asset // inherits from Asset
{
	public long SharesOwned;
}

public class House : Asset // inherits from Asset
{
	public decimal Mortgage;
}

```

# Polymorphism
```cs
public static void Display (Asset asset)
{
	System.Console.WriteLine (asset.Name);
}


Stock msft = new Stock ... ;
House mansion = new House ... ;
Display (msft);
Display (mansion);
``

## Upcasting
```cs
Stock msft = new Stock();
Asset a = msft; // Upcast
Console.WriteLine (a == msft); // True
Console.WriteLine (a.Name); // OK
Console.WriteLine (a.SharesOwned); // Error: SharesOwned undefined
```

## Downcasting
```cs
Stock msft = new Stock();
Asset a = msft; // Upcast
Stock s = (Stock)a; // Downcast
Console.WriteLine (s.SharesOwned); // <No error>
Console.WriteLine (s == a); // True
Console.WriteLine (s == msft); // True
```

```cs
House h = new House();
Asset a = h; // Upcast always succeeds
Stock s = (Stock)a; // Downcast fails: a is not a Stock
```

## The as operator
```cs
Asset a = new Asset();
Stock s = a as Stock; // s is null; no exception thrown

int shares = ((Stock)a).SharesOwned; // Approach #1
int shares = (a as Stock).SharesOwned; // Approach #2
```

## The is operator
```cs

```




## Virtual Function Members
```cs
```

### Abstract Classes and Abstract Members
```cs
public abstract class Asset
{
	// Note empty implementation
	public abstract decimal NetValue { get; }
	}
	
	public class Stock : Asset
	{
		public long SharesOwned;
		public decimal CurrentPrice;
	
		// Override like a virtual method.
		public override decimal NetValue
		{
			get { return CurrentPrice * SharesOwned; }
		}
	}		
}
```


### Hiding Inherited Members
```cs
public class A { public int Counter = 1; }
public class B : A { public int Counter = 2; }

public class A { public int Counter = 1; }
public class B : A { public new int Counter = 2; }
```

### Sealing Functions and Classes
```cs
public sealed override decimal Liability { get { return Mortgage; } }
```

#### The base Keyword
```cs
public class House : Asset
{
	...
	public override decimal Liability
	{
		get { return base.Liability + Mortgage; }
	}
}
```

### Constructors and Inheritance
```cs
public class Baseclass
{
	public int X;
	public Baseclass () { }
	public Baseclass (int x) { this.X = x; }
}
public class Subclass : Baseclass { }

public class Subclass : Baseclass
{
	public Subclass (int x) : base (x) { }
}
```

### Boxing and Unboxing
```cs
int x = 9;
object obj = x; // Box the int

int y = (int)obj; // Unbox the int
```
### Copying semantics of boxing and unboxing



## Interfaces
```cs
public interface IEnumerator
{
	bool MoveNext();
	object Current { get; }
	void Reset();
}

internal class Countdown : IEnumerator
{
	int count = 11;
	public bool MoveNext () { return count-- > 0 ; }
	public object Current { get { return count; } }
	public void Reset() { throw new NotSupportedException(); }
}

IEnumerator e = new Countdown();
while (e.MoveNext())
	Console.Write (e.Current); // 109876543210
```	
	
### Extending an Interface	
```cs
public interface IUndoable { void Undo(); }
public interface IRedoable : IUndoable { void Redo(); }
```

### Explicit Interface Implementation
```cs
interface I1 { void Foo(); }
interface I2 { int Foo(); }

public class Widget : I1, I2
{
	public void Foo ()
	{
		Console.WriteLine ("Widget's implementation of I1.Foo");
	}
	
	int I2.Foo()
	{
		Console.WriteLine ("Widget's implementation of I2.Foo");
		return 42;
	}
}


Widget w = new Widget();
w.Foo(); // Widget's implementation of I1.Foo
((I1)w).Foo(); // Widget's implementation of I1.Foo
((I2)w).Foo(); // Widget's implementation of I2.Foo
```

### Implementing Interface Members Virtually
```cs
public interface IUndoable { void Undo(); }
public class TextBox : IUndoable
{
	public virtual void Undo()
	{
		Console.WriteLine ("TextBox.Undo");
	}

}

public class RichTextBox : TextBox
{
	public override void Undo()
	{
		Console.WriteLine ("RichTextBox.Undo");
	}
}

RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo
((IUndoable)r).Undo(); // RichTextBox.Undo
((TextBox)r).Undo(); // RichTextBox.Undo
```

### Reimplementing an Interface in a Subclass
```cs
public interface IUndoable { void Undo(); }
public class TextBox : IUndoable
{
void IUndoable.Undo() { Console.WriteLine ("TextBox.Undo"); }
}
public class RichTextBox : TextBox, IUndoable
{
public new void Undo() { Console.WriteLine ("RichTextBox.Undo"); }
}

RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo Case 1
((IUndoable)r).Undo(); // RichTextBox.Undo Case 2


public class TextBox : IUndoable
{
public void Undo() { Console.WriteLine ("TextBox.Undo"); }
}


RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo 				Case 1
((IUndoable)r).Undo(); // RichTextBox.Undo 	Case 2
((TextBox)r).Undo(); // TextBox.Undo		Case 3
```

### Alternatives to interface reimplementation
```cs
public class TextBox : IUndoable
{
	void IUndoable.Undo() { Undo(); } // Calls method below
	protected virtual void Undo() { Console.WriteLine ("TextBox.Undo"); }
}

public class RichTextBox : TextBox
{
	protected override void Undo() { Console.WriteLine("RichTextBox.Undo"); }
}
```


## Access Modifiers 
```cs
namespace AccessModifiers
{
    class Modifiers
    {
		//Method AAA is not marked with any access modifier which automatically makes it private, that is the default.
		//Method BBB can access AAA but other class can't
        static void AAA()
        {
            Console.WriteLine("Modifiers AAA");
        }

        public static void BBB()
        {
            Console.WriteLine("Modifiers BBB");
            AAA();
        }
    }

     class Program
    {
        static void Main(string[] args)
        {
            Modifiers.BBB();
        }
    }
}
//Output
//Modifiers BBB
//Modifiers AAA

```   

```cs
class Program
{
	static void Main(string[] args)
	{
		Modifiers.AAA();
		Console.ReadKey();
	}
}
//Output
//'AccessModifiers.Modifiers.AAA()' is inaccessible due to its protection level

```


```cs
class Modifiers
{
	protected static void AAA()
	{
		Console.WriteLine("Modifiers AAA");
	}

	public static void BBB()
	{
		Console.WriteLine("Modifiers BBB");
		AAA();
	}
}
	

class Program
{
    static void Main(string[] args)
    {
        Modifiers.AAA();
        Console.ReadKey();
    }
}
//Output
'AccessModifiers.Modifiers.AAA()' is inaccessible due to its protection level	
```

### Modifiers in Inheritance
```cs
//Modifiers Base Class
class ModifiersBase
{
	static void AAA()
	{
		Console.WriteLine("ModifiersBase AAA");
	}
	public static void BBB()
	{
		Console.WriteLine("ModifiersBase BBB");
	}
	protected static void CCC()
	{
		Console.WriteLine("ModifiersBase CCC");
	}
}
	
//Modifiers Derive Class

class ModifiersDerived:ModifiersBase
{
    public static void XXX()
    {
        AAA();
        BBB();
        CCC();
    }
}

//Program Class
class Program
{
    static void Main(string[] args)
    {
        ModifiersDerived.XXX();
        Console.ReadKey();
    }
}
```


### Namespaces with Modifiers
```cs
public namespace AccessModifiers
{
    class Program
    {
        static void Main(string[] args)
        {

        }
    }
}

//Output
Compile time error: A namespace declaration cannot have modifiers or attributes
```


### Private Class
```cs
namespace ConsoleApplication2
{
    private class ModifiersBase
    {
        public static void BBB()
        {
            Console.WriteLine("ModifiersBase BBB");
        }
    }
}	

Output
Compile time error: Elements defined in a namespace cannot be explicitly declared as private, protected, or protected internal
```


### Internal Class and Public Method
```cs
namespace AccessModifiersLibrary
{
    internal class ClassA
    {
        public void MethodClassA(){}
    }
}


using AccessModifiersLibrary;

namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA = new ClassA();
            classA.MethodClassA();
        }
    }
}

//Output
'AccessModifiersLibrary.ClassA' is inaccessible due to its protection level
The type 'AccessModifiersLibrary.ClassA' has no constructors defined
'AccessModifiersLibrary.ClassA' is inaccessible due to its protection level
'AccessModifiersLibrary.ClassA' does not contain a definition for 'MethodClassA' and
no extension method 'MethodClassA' accepting a first argument of type 'AccessModifiersLibrary.ClassA'
could be found (are you missing a using directive or an assembly reference?)
```


### Public Class and Private Method
```cs
AccessModifiersLibrary.ClassA:

namespace AccessModifiersLibrary
{
    public class ClassA
    {
        private void MethodClassA(){}
    }
}


using AccessModifiersLibrary;

 namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA = new ClassA();
            classA.MethodClassA();
        }
    }
}


//Output on compilation
'AccessModifiersLibrary.ClassA' does not contain a definition
for 'MethodClassA' and no extension method 'MethodClassA' accepting a first argument
of type 'AccessModifiersLibrary.ClassA' could be found (are you missing a using directive or an assembly reference?)
```


### Public Class and Internal Method
```cs
AccessModifiersLibrary.ClassA:

namespace AccessModifiersLibrary
{
    public class ClassA
    {
        Internal void MethodClassA(){}
    }
}


using AccessModifiersLibrary;

 namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA = new ClassA();
            classA.MethodClassA();
        }
    }
}

//Output on compilation
'AccessModifiersLibrary.ClassA' does not contain a definition for 'MethodClassA' and no extension
method 'MethodClassA' accepting a first argument of type 'AccessModifiersLibrary.ClassA' could be
found (are you missing a using directive or an assembly reference?)
```


### Protected Internal
```cs
namespace AccessModifiersLibrary
{
    public class ClassA
    {
        protected internal void MethodClassA()
        {

        }
    }

    public class ClassB:ClassA
    {
        protected internal void MethodClassB()
        {
            MethodClassA();
        }
    }

    public class ClassC
    {
        public void MethodClassC()
        {
            ClassA classA=new ClassA();
            classA.MethodClassA();
        }
    }
}



using AccessModifiersLibrary;

 namespace AccessModifiers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            ClassC classC=new ClassC();
            classC.MethodClassC();
        }
    }
}

//Compiler output
The code successfully compiles with no error.
```


### Sealed Classes

```cs
namespace AccessModifiers
{
    sealed class AAA
    {
        public int x = 100;
        public void MethodA()
        {
            Console.WriteLine("Method A in sealed class");
        }
    }
    public class Program
    {
        public static void Main(string[] args)
        {
            AAA aaa=new AAA();
            Console.WriteLine(aaa.x);
            aaa.MethodA();
            Console.ReadKey();
        }
    }
}
//Compiler Output
//100
//Method A in sealed class
```
	
	
```cs	
 namespace AccessModifiers
{
    sealed class AAA
    {

    }
    class BBB:AAA
    {

    }
    public class Program
    {
        public static void Main(string[] args)
        {
        }
    }
}

//Compiler Output
'AccessModifiers.BBB': cannot derive from sealed type 'AccessModifiers.AAA'	
```


### Constants
```cs
public class Program
 {
     private const int x = 100;
     public static void Main(string[] args)
     {
         Console.WriteLine(x);
         Console.ReadKey();
     }
 }
 Output
 100 
 ```
 
 ```cs
 namespace AccessModifiers
{
    public class Program
    {
        private const int x = y + 100;
        private const int y = z - 10;
        private const int z = 300;

        public static void Main(string[] args)
        {
           System.Console.WriteLine("{0} {1} {2}",x,y,z);
            Console.ReadKey();
        }
    }
}

Output
390 290 300
```

```cs
namespace AccessModifiers
{
    public class Program
    {
        private const int x = y + 100;
        private const int y = z - 10;
        private const int z = x;

        public static void Main(string[] args)
        {
           System.Console.WriteLine("{0} {1} {2}",x,y,z);
            Console.ReadKey();
        }
    }
}
Output
The evaluation of the constant value for 'AccessModifiers.Program.x' involves a circular definition
```

```cs
//A const is a variable whose value once assigned cannot be modified, but its value is determined at compile time only.
namespace AccessModifiers
{
    public class Program
    {
        public const ClassA classA=new ClassA();
        public static void Main(string[] args)
        {
        }
    }

   public class ClassA
    {

    }
}
//Output
Compile time error: 'AccessModifiers.Program.classA' is of type 'AccessModifiers.ClassA'.
A const field of a reference type other than string can only be initialized with null.
```

```cs
public class ClassA
    {
        public const int aaa = 10;
    }
	
	public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA=new ClassA();
            Console.WriteLine(classA.aaa);
            Console.ReadKey();
        }
    }

Output
Compile time error: Member 'AccessModifiers.ClassA.aaa'
cannot be accessed with an instance reference; qualify it with a type name instead 
```

```cs
//Just mark the const as static.
using System;
namespace AccessModifiers
{
    public class ClassA
    {
        public static const int aaa = 10;
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            ClassA classA=new ClassA();
            Console.WriteLine(classA.aaa);
            Console.ReadKey();
        }
    }
}

Output
Compile time error: The constant 'AccessModifiers.ClassA.aaa' cannot be marked static
```

```cs
namespace AccessModifiers
{
    public class ClassA
    {
        public const int xxx = 10;
    }

    public class ClassB:ClassA
    {
        public const int xxx = 100;
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine(ClassA.xxx);
            Console.WriteLine(ClassB.xxx);
            Console.ReadKey();
        }
    }
}
Output
10
100
Compiler Warning: 'AccessModifiers.ClassB.xxx' hides inherited
member 'AccessModifiers.ClassA.xxx'. Use the new keyword if hiding was intended.
```


## Static Fields
```cs
namespace AccessModifiers
{
    public class Program
    {
        private static int x;
        private static Boolean y;
        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.WriteLine(y);
            Console.ReadKey();
        }
    }
}

Output
0
False
```

```cs
namespace AccessModifiers
{
    public class Program
    {
         int x = y + 10;
         int y = x + 5;
        public static void Main(string[] args)
        {

        }
    }
}

Output
Compile time error:
A field initializer cannot reference the non-static field, method, or property 'AccessModifiers.Program.y'
A field initializer cannot reference the non-static field, method, or property 'AccessModifiers.Program.x'
```

### Readonly Fields
```cs
namespace AccessModifiers
{
    public class Program
    {
        public static readonly int x = 100;

        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.ReadKey();
        }
    }
}

Output
100
```

```cs
namespace AccessModifiers
{
    public class Program
    {
        public static readonly int x = 100;

        public static void Main(string[] args)
        {
            x = 200;
            Console.WriteLine(x);
            Console.ReadKey();
        }
    }
}

Output
Compile time error: A static readonly field cannot be assigned to
(except in a static constructor or a variable initializer).
```


```cs
namespace AccessModifiers
{
    public class Program
    {
        public static readonly int x;

        static Program()
        {
            x = 100;
            Console.WriteLine("Inside Constructor");
        }

        public static void Main(string[] args)
        {
            Console.WriteLine(x);
            Console.ReadKey();
        }
    }
}
Inside Constructor
100
```

```cs
namespace AccessModifiers
{
    public class ClassA
    {
        public int readonly x= 100;
    }
    public class Program
    {
      public static void Main(string[] args)
        {
        }
    }
}

Output
Compile time error:
Member modifier 'readonly' must precede the member type and name
Invalid token '=' in class, struct, or interface member declaration
```