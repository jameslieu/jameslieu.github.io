---
layout: post
title: "Inversion of Control (IoC)"
categories: Programming
excerpt: What is the IoC principle and why is it useful?
---

Upon attempting to understand inversion of control, I stumbled across a few buzz words which are related but not quite the same, which can get confusing and so I decided to share my learning on some of these terms, what they are and why they're useful in programming.

The four terms I'm going to briefly cover are:
- &#x1f504; Inversion of Control (IoC)
- &#x1f91d; Dependency Inversion (DIP)
- &#x1f489; Dependency Injection (DI)
- &#x1f5f3; IoC Container

## Inversion of Control &#x1f504;

Inversion of control (IoC) is a programming principle and is used to invert different types of controls in object oriented design to achieve loose coupling. "Control" refers to any additional responsibilities a class has outside of it's main responsibility.

IoC is all about inverting the control. In layman's terms, suppose you drive a car to work. The IoC principle suggests to invert the control, meaning that instead of driving the car yourself to get to work, you can get taxi where somebody else will be driving the car. You wouldn't be driving yourself and so you can focus on your main responsibilities.

The IoC principle helps in designing loosely coupled classes which make them testable, maintainable and extensible.

## Dependency Inversion Principle &#x1f91d;
The dependency inversion principle (DIP) is one of the SOLID object-oriented principle invented by Robert Martin (a.k.a. Uncle Bob).
The definition of DIP is
1. High-level modules should not depend on low-level modules. Both should depend on the abstraction.
2. Abstractions should not depend on details. Details should depend on abstractions.

#### What is an abstraction?
Abstraction means something which is non-concrete. When you can create an object from something such as a class, that is considered a concretion, and so abstraction in programming is to create an interface or abstract class which are non-concrete and you wouldn't be able to instantiate it.

You cannot create an object of an interface or abstract class. As per DIP, modules should not depend of concrete classes, they should depend on interfaces or an abstract class.

The advantages of implementing DIP is classes are loosely coupled  and will not depend on any concrete class but instead includes a reference to an interface. This then means that we can, if necessary, use another class which **implements** that interface with a different implementation.

## Dependency Injection &#x1f489;

Dependency Injection (DI) is a design pattern used to implement IoC. It allows the creation of dependent objects outside of a class and provides those objects to a class through different ways. Using DI, we move the creation and binding of the dependent objects outside of the class that depends on them.

#### Types of Dependency Injection

- Constructor Injection: The injector supplies the dependency through the class constructor.
- Property Injection: The injector supplies the dependency through a public property of the client class.
- Method Injection: The class implements an interface which declares the methods to supply the dependency and the injector uses this interface to supply the dependency.

In professional projects, there are many dependent classes and implementing these patterns is time consuming. Here the IoC Container (aka the DI container) helps us.

## IoC Container &#x1f5f3;

IoC Container, also known as DI Container, is a framework for implementing **automatic** dependency injection. It managed object creation and it's life-time, and also injects dependencies to the class.

The IoC container creates an object of the specified class and also injects all the dependency objects through a constructor, a property or method at run time and disposes it at the appropriate time. This is done so we don't have to create and manage objects manually.

### DI lifecycle

#### &#x1f4cb; Register
The container must know which dependency to instantiate when it encounters a particular type. The process is called registration.

#### &#x1f3cb; Resolve
When using the IoC container, we don't need to create objects manually, the container does it automatically. This is called resolution. The container creates an object of the specified type, injects the required dependencies if any and returns the object.

#### &#x1f5d1; Dispose
The container will manage the lifetime of the dependent objects. Most IoC containers include lifetime managers to manage an object's lifecycle and dispose it.