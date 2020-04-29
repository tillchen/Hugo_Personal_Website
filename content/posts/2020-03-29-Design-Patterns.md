+++
draft = false
date = 2020-03-29
title = "Design Patterns"
description = "Some notes for design patterns"
tags = ["Software Engineering"]
+++

* [Basics](#basics)
* [The Observer Pattern](#the-observer-pattern)
* [The Decorator Pattern](#the-decorator-pattern)
* [The Factory Pattern](#the-factory-pattern)
* [The Singleton Pattern](#the-singleton-pattern)
* [The Command Pattern](#the-command-pattern)
* [The Adapter Pattern](#the-adapter-pattern)
* [The Facade Pattern](#the-facade-pattern)
* [The Template Method Pattern](#the-template-method-pattern)
* [The State Pattern](#the-state-pattern)
* [The Proxy Pattern](#the-proxy-pattern)
* [Model-View-Controller](#model-view-controller)
* [Design Patterns](#design-patterns)
* [References](#references)

## Basics

1. Identify the varying parts and separate them from the invariant.

2. Program to an interface (supertype), not an implementation.

    ```java
    Animal animal = new Dog();
    animal.makeSound();
    List<Integer> list = new ArrayList<Integer>();
    ```

3. Favor composition over inheritance. HAS-A can be better than IS-A.

4. The strategy pattern enables selecting an algorithm at runtime. Instead of implementing a single algorithm directly, code receives run-time instructions as to which in a family of algorithms to use.

## The Observer Pattern

1. Publishers (Subject) + Subscribers (Observers) = Observer Pattern.

2. It defines a one-to-many dependency. When the subject changes, all dependents are notified.

3. This enables loose coupling, which minimizes the interdependency between objects.

4. In Java, we can use the built-in Observable - Observer superclasses.

    ```java
    // extends Observable
    setChanged();
    notifyObservers();
    // extends Observer
    // in the constructor
    observable.addObserver(this);
    ```

5. In Java, Observable is a class, which means we have to subclass it.

6. UML:
   * ![Observer](/images/observer.png)
   * Example: ![Observer example](/images/observer_example.png)

## The Decorator Pattern

1. **The open-closed principle**: classes should be open for extension, but closed for modification.

2. Decorators have the same supertype as the object they decorate.

3. You can use one or more decorators to wrap (HAS-A) an object.

4. The decorator adds its own behavior either before and/or after delegating to the object it decorates to do the rest of the job.

5. The decorator pattern attaches additional responsibilities to an object dynamically.

6. UML:
   * ![Decorator](/images/decorator.png)
   * Example: ![Decorator example](/images/decorator_example.png)

7. `java.io` is mainly using the decorator pattern.

## The Factory Pattern

1. The factory method pattern defines an interface for creating an object, but lets subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

2. UML:
   * ![Factory](/images/factory.png)
   * Example: ![Factory example](/images/factory_example.png)

3. **The dependency inversion principle**: Depend upon abstractions. Do not depend upon concrete classes. High-level components should not depend on low-level components; rather, they should both depend on abstractions.
    * No variables should hold a reference to a concrete class.
    * No class should derive from a concrete class.

4. The abstract factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

## The Singleton Pattern

1. The singleton pattern restricts the instantiation of a class to one single instance, and provides a global point of access to it:

    ```java
    public class Singleton {
        private static Singleton uniqueInstance;
        private Singleton() {} // PRIVATE constructor
        public static synchronized Singleton getInstance() { // remove synchronized if there's no multithreading
            if (uniqueInstance == null) {
                uniqueInstance = new Singleton();
            }
            return uniqueInstance;
        }
    }
    ```

## The Command Pattern

1. The command pattern encapsulates a request as an object, thereby letting you parameterize other objects with different requests and support undoable operations.

2. UML:
   * ![Command](/images/command.png)

## The Adapter Pattern

1. The adapter pattern converts the interface of a class into another interface the clients expect. It lets classes work together that couldn't otherwise because of incompatible interfaces.

2. UML:
   * ![Adapter1](/images/adapter1.png)
   * ![Adapter2](/images/adapter2.png)

## The Facade Pattern

1. The facade pattern provides a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

2. **Principle of Least Knowledge**: talk only to your immediate friends.

## The Template Method Pattern

1. The template method pattern defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure:

    ```java
    abstract class AbstractClass {
        final void templateMethod() {
            primitiveOperation1();
            primitiveOperation2();
            concreteOperation();
        }

        abstract void primitiveOperation1();

        abstract void primitiveOperation2();

        void concreteOperation() {
            // implementation here
        }
    }
    ```

2. **The Hollywood Principle (aka. Inversion of Control)**: (High-level components) Don't call us, we'll call you (low-level components).

3. **Single responsibility:**: a class should have only one reason to change.

## The State Pattern

1. The state pattern allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

2. It's close to the concept of finite-state machines.

## The Proxy Pattern

1. A remote proxy acts as a local representative to a remote object.

2. Java RMI's (remote method invocation) client helper is a "stub" and the service helper is a "skeleton". The stub is the proxy.

3. The proxy pattern provides a surrogate or placeholder for another object to access it.

## Model-View-Controller

1. The MVC is using:
    * the strategy pattern: the view delegates to the controllers to handle user actions. (Swappable controllers.)
    * the composite pattern: the view is a composite of GUI components.
    * the observer pattern: the model is the observable, and the view & controller are observers.

## Design Patterns

1. Categories:
    * Creational: Factory, Singleton
    * Behavioral (how classes communicate): State, Iterator, Command
    * Structural: Adapter, Composite, Decorator, Facade, Proxy

## References

* [Head First Design Patterns: A Brain-Friendly Guide 1st Edition](https://www.amazon.com/Head-First-Design-Patterns-Brain-Friendly-dp-0596007124/dp/0596007124/ref=mt_paperback?_encoding=UTF8&me=&qid=1585509064)
