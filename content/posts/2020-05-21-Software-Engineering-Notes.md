+++
draft = false
date = 2020-05-21
title = "Software Engineering Notes"
description = "This is the course notes for Software Engineering at Jacobs University Bremen."
tags = ["Software Engineering"]
+++

* [Introduction](#introduction)
  * [Intro](#intro)
  * [Socio-Technical Systems](#socio-technical-systems)
* [The Software Lifecycle](#the-software-lifecycle)
  * [Software Lifecycle](#software-lifecycle)
  * [Requirements Engineering](#requirements-engineering)
  * [UML](#uml)
  * [Design Patterns](#design-patterns)
  * [Compiling and Linking](#compiling-and-linking)
  * [Defensive Programming](#defensive-programming)
  * [Configuration, Version, and Release Management](#configuration-version-and-release-management)
* [Web and Other Applications](#web-and-other-applications)
* [Project and Process Management](#project-and-process-management)
* [Security and Ethics](#security-and-ethics)

## Introduction

This is the course notes for Software Engineering at Jacobs University Bremen.

### Intro

1. The code-and-fix cycle:
    * Maintainability and reliability decrease continuously (entropy).
    * If the programmer leaves, all know-how leaves.
    * If the developer is not the user, we get frequent dissent about expectations vs implementations.

2. Common problems:
    * Complexity
    * Integration requirements
    * Quality requirements
    * Flexibility requirements
    * Portability and internationalization requirements
    * Organizational requirements
      * Communication problems/ bad project management

3. Software engineering is multi-person construction of multi-version software

4. Software = programs + documentation

5. System engineering = hardware + software + process engineering

6. Good software delivers functionality and performance that is (MEDA)
    * Maintainable
    * Efficient
    * Dependable
    * Acceptable

### Socio-Technical Systems

1. System = software + hardware + people

2. System categories:
    * Technical = software + hardware
    * Socio-technical = technical systems + operational processes & people

3. Socio-technical system characteristics:
    * Emergent properties
    * Non-deterministic
      * Partially dependent on human operators + a time-varying environment
    * Complex relationships with organizational objectives

## The Software Lifecycle

### Software Lifecycle

1. Requirements Engineering
2. Design
3. Coding
4. Verification & Testing
5. Deployment & Maintenance

### Requirements Engineering

1. Requirements engineering = services + constraints

2. Types of requirements:
    * User requirements - understandable by users (UML)
    * System requirements

3. Another way of classification:
    * Functional requirements
    * Non-functional requirements - properties + constraints
    * Domain requirements

### UML

1. Use case diagrams
    * Use case = a chunk of functionality
    * Actor = someone/something that interacts with the system

2. Activity diagrams
    * Represents the overall flow of control
    * User-perceived actions

3. Class diagrams: <https://creately.com/blog/diagrams/class-diagram-relationships/>
    * Relationships:
      * Association - connection
      * Aggregation - stronger: HAS-A
      * Dependency - weaker
    * Arrow head means it's traversable only this direction

4. Sequence diagrams: object interactions in a time sequence
    * Actors + system components (unlike activity diagrams)

5. State transition diagrams: lifecycle of a given class

6. Alternative: DSLs (domain specific modelling languages)
    * Better used for embedded systems

### Design Patterns

1. Pattern = description + essence of its solution

2. Design pattern = re-using abstract knowledge; generic, reusable design templates for OOP

3. Singleton: ensure a class has only one instance and provide a global access point

4. Observer: separate the display of object state from the object itself

5. Mediator: define an object that encapsulates how a set of objects interact
    * Loose coupling

6. Facade: a unified interface to a set of interfaces in a subsystem
    * Loose coupling

7. Proxy: a surrogate or placeholder for another object to control access to it

8. Adapter: let classes work together that could not otherwise because of incompatible interfaces

9. Composite: compose objects into tree structures to represent part-whole hierarchies

10. Types:
    * Creational
    * Structural
    * Behavioral

### Compiling and Linking

1. source + header files -> Preprocessor -> source -> compiler -> object code -> linker -> executable

2. Preprocessor: textual substitution (with directives #)

3. Object files contain code for a program fragment.

4. Name mangling (name decoration): compiler modifies names to make them unique

5. Linker generates one executable from several object and library files.

6. Strip:
    * By default, executables contain symbol tables which allows reverse engineering and makes the code files substantially larger.
    * Strip executables before shipping

7. Library = archive file containing a collection of object files
    * Object files are linked in completely, from library only what is actually needed

### Defensive Programming

1. Defensive programming intends to ensure the continuing function of the software despite the unforeseeable usage. - Defend against errors (avoid bugs)

2. Invariants:
    * Loop invariants
    * Class invariants: true before and after each method call
    * Method invariants: meet the pre and post conditions - part of design-by-contract (methods are contracts with the user)
    * Ways of enforcing invariants
      * Assertions
      * Exceptions
      * Return codes

3. Structured programming: only use a small set of programming constructs
    * Good: sequence, condition, repetition
    * Bad: goto, break, continue

4. Code guide = uniform style + best practice

### Configuration, Version, and Release Management

1. Software configuration management (SCM) is the discipline of controlling the evolution of software systems.

2. Three classic problems:
    * The double maintenance problem
    * The shared data problem
    * The simultaneous update problem

3. A delta is a difference between two revisions.

4. Terminology:
    * Release: a version that's available to user/client
    * Configuration: combination of components into a system according to case-specific criteria
    * Baseline: a static reference point

5. Configuration models:
    * Composition model = set of objects -- module oriented
    * Change set model = bundle of changes -- dynamic
    * Long transaction model = all changes all isolated into transactions -- collaborative

## Web and Other Applications

## Project and Process Management

## Security and Ethics
