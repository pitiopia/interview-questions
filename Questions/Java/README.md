# Java Interview Questions

Below you can find a list of most common questions that might occur during Java Interview.

This file is a part of bigger set of [IT Interview Questions](../../README.md)

# Questions

#### Define HashMap in Java

HashMap is a data structure that stores key/value pairs.
It gives the ability to add new data and search the collection by particular key in constant time.
On the other hand it does not preserve the order of added data.

#### What is the difference between HashMap and HashTable

In general HashMap is a newer version of HashTable with some differences:

HashTable | HashMap
--------- | ----------
thread safe (synchronized) | non thread safe (not synchronized)
slower (allows only operations by one thread at a time) | faster ( multiple threads can operate on it at the same time )
doesn't allow null key nor null values | allows single null key and multiple null values
implements Enumeration interface | implements Iterator interface

#### What is the difference between ArrayList and Vector

We can say that ArrayList is for Vector the same as HashMap is for HashTable:

Vector | ArrayList
-------- | -------
thread safe (synchronized) | non thread safe (not synchronized)
slower (allows only operations by one thread at a time) | faster ( multiple threads can operate on it at the same time )
implements Enumeration interface | implements Iterator interface

#### What is an immutable object?

* object that can't be modified once created
* any modification of immutable object results in creating new object
* String object is a good example of an immutable object

#### What is the difference between local/instance/class variables?

Local variable:
* defined inside a method
* has to be initialized before it is used (otherwise generates compiler error)
* doesn't have default value

Instance variable:
* defined inside class definition (but outside method definition)
* is created when object is being instantiated
* doesn't have to be initialized
* is given default value depending of variable type

Class variable:
* defined inside class definition (but outside method definition)
* is being preceded by `static` keyword
* is shared across multiple objects
* doesn't have to be initialized
* is given default value

Default values of class/instance variables depending on type:

Type | Default value
----- | --------
boolean | false
byte/short/int/long | 0
float/double | 0.0
char | '\u0000' NUL
object | null

#### What are access modifiers?

Access modifiers define the accessibility of a given method or class property for a potential caller.
We have 4 different access modifiers in Java (sorted by their accessibility descending):
* `public` - it is accessible from any class in the program
* `default` ( used by leaving access modifier blank ) - it is accessible only by the class, subclass and any class from the same package
* `protected` - it is accessible from the class and all its subclasses
* `private` - it is accessible only by the main class

#### What is `finalize()` method for?

`finalize()` is a method that can be implemented in any class. Its job is to run additional code just before the destruction of the object.
It can (but not have to) be called before the object is being destroyed. It all depends if the garbage collector tries to collect this object or not.