---
author: arul
category:
  - software-development
cover:
  alt: object-oriented
  image: /wp-content/uploads/2013/12/object-oriented.jpg
date: "2013-12-04T13:14:53+00:00"
guid: http://arul.pw/?p=51
tag:
  - oops
  - programing-basic
title: Object-Oriented Programming Basic
url: /object-oriented-programming-basic/

---
This article is for people who want to learn the basics before entering into programming life or who want to learn the foundation for programming. Any language can be chosen only if you are strong in the concept before writing your code and automatically your code will be more powerful and reusable. Below are the examples which I  used for C# Language.

**What is Oops?**

Oops is a paradigm that is used while designing applications and computer programs. C# also provides full support for, Oops.

Basic Oops Concepts:

- **Classes and Object**
- **Data Abstraction and Encapsulation**
- **Inheritance**
- **Polymorphism**

### Classes and Object

#### Class:

Class is a type of object or you can call it as a blueprint for the object instance, as how a blueprint is created before building the house.

[![bluePrint](/wp-content/uploads/2013/12/bluePrint-300x186.jpg)](http://arul.pw/wp-content/uploads/2013/12/bluePrint.jpg)

Example:

```
class DreamHome
{
}
```

#### Object

Objects are usable instance of classes. It’s a building made from the blueprint called class. Its not logical rather it's a physical existence that you can enter inside home and use all the properties that belong to it.

[![home](/wp-content/uploads/2013/12/home-300x234.jpg)](http://arul.pw/wp-content/uploads/2013/12/home.jpg)

Example:

```
DreamHome myHome=new DreamHome();
```

myHome is the instance of class type DreamHome. So myHome is built based on DreamHome blueprint.

**Note:**

class is a logical and object is a physical existence.

#### Member of Class:

- Properties and Fields (To describe class data)
- Methods(To describe class behavior)
- Events(To Provide communication b/w different class and objects)

### Data Abstraction and Encapsulation

#### **Data Abstraction:**

It's a technique that is designed to separate interface and implementation, i.e, providing essential information to outside world and hiding the background implementations.

[![Interface](/wp-content/uploads/2013/12/Interface-300x199.jpg)](http://arul.pw/wp-content/uploads/2013/12/Interface.jpg)

       In the above picture, smart TV  is controlled by remote, so remote is the interface for remote user and TV. Here actual implementation is hidden from user and thereby user takes control of TV with limited facility that is available on remote, but user can't control TV's hardware which is present inside TV.

#### Encapsulation :

It's a group of related properties, methods and other members that acts as a single unit or object.

 [![Capsule](/wp-content/uploads/2013/12/capsule-300x201.jpg)](http://arul.pw/wp-content/uploads/2013/12/capsule.jpg)

**Interface Example:**

It's a communication point to the outside world.

```
interface IGuest
{
   bool CallingBell(string name);
   bool OpenMainGate(string key);
   bool EnterHall();
}
public class DreamHome:IGuest
{
   public string TV{get;set;}
   public string Sofa{get;set;}
   public Object BedRoom{get;set;}
   public int Money{get;set;}

   public bool CallingBell(string name)
   {
     //Calling bell is ringing
     return true;
   }
   public bool OpenMainGate(string key)
   {
     //logic to open the gate
     return true;
   }
   public bool EnterHall()
   {
     //Logic to come inside Hall
     return true;
   }
   public bool EnterBedRoom()
   {
      //Login to come inside bed room
      return true;
   }
   public int GetMoney()
   {
      //Login to withdraw amount  return 2000;
   }
}
class Program
{
   static void Main(string[] args)
   {
      IGuest guest = new DreamHome();
      guest.CallingBell("uncle"); // return true
      guest.GetMoney(); // Error your Unclue don't have the privilage to get the money from your home-
   }
}
```

In the above example, we have an interface called IGuest, which was implemented in the Home class. When a guest comes to our home they have only limited access to our home. We will not allow them to access private areas(bedrooms) and only a limited facility is exposed for them. From the above example, we have more methods but the guest has access only to CallingBell, OpenMainGate, and EnterHall. So the guest can't enter the bedroom.

Inheritance

Inheritance enables us to create new classes that can be reusable, extend, and modify the behavior that is defined in the base classes.

**Example:**

```
   public class OldHome
    {
        public string Fridge { get; set; }
        public string DVDPlayer{ get; set; }
    }
    public class DreamHome:OldHome
    {
        public string TV{ get; set; }
        public string Sofa{ get; set; }
        public string BedRoom{ get; set; }
        public float Money{ get; set; }
    }
    class Program
    {
        static void Main(string[] args)
        {
            DreamHome myHome= new DreamHome();
            myHome.Fridge ="Samsung";
        }
    }
```

In the above example DreamHome class is inherited from the OldHome. So all the properties and members that belong to OldHome are accessible for the DreamHome. For example, we are re-using the fridge that we already used in our old home to our new DreamHome, which directly means that there is no requirement to buy a new one.

Types of Inheritance

1. Single Inheritance
1. Multilevel Inheritance
1. Hierarchical Inheritance
1. Hybrid Inheritance
1. Multiple Interface

### Polymorphism

Polymorphism is a third pillar of object-oriented programming, after encapsulation and inheritance. It gives ability of an object or reference to take many different forms at different instances.It has two category: compile time and run time

**Compile Time Polymorphism**:

The decision will be made at compile time.

Example:

Method overloading:

```
class program
{
    public class DreamHome
        {

            public void GetObject(int amount)
            {
                 //get the amount
            }

            public void GetObject(string fridge)
            {
                //get the samsungfridge logic
            }

        }

        static void Main(string[] args)
        {
            DreamHome obj = new DreamHome();

            obj.GetObject(1000);  //get the amount 1000 from the DreamHome

            obj.GetObject("Samsung");  //get the samsung fridge from the DreamHome

        }
    }
```

In the example we have two methods with same name, but the parameter is different so compiler will decide which method has to invoke in the compile time itself based on the input method param.

 **Run Time Plymorphism:**

The decision made at Run time.

```
class Program
{
   public class OldHome
   {
         public virtual void WatchTV()
         {
               Console.WriteLine("watch the program in the old black and white tv");
         }
   }
   public class DreamHome : OldHome
   {
          public override void WatchTV()
          {
               Console.WriteLine("watch the program in the new LED TV");
          }
  }
  static void Main(string[] args)
  {
          OldHome objBase = new OldHome();
          objBase.WatchTV();// Output ----> watch the program in the old black and white tv

          objBase = new DreamHome();
          objBase.WatchTV();//Output--> watch the program in the new LED TV.

           Console.ReadLine();
  }
}
```

In the above example "Watch TV" method will be invoked in run time based on the instance created. If you enter DreamHome you can watch the TV Program in new LED Tv or if you enter Old home you can watch the program in old black and white TV. It's the same method we implement here. But based on instance the decision will be made at application run time.
