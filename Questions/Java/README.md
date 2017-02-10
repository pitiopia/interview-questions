# Java Interview Questions

Below you can find a list of most common questions that might occur during Java Interview.

This file is a part of bigger set of [IT Interview Questions](../../README.md)

# Questions

#### :bangbang: Define HashMap in Java :bangbang:

HashMap is a data structure that stores key/value pairs.
It gives the ability to add new data and search the collection by particular key in constant time.
On the other hand it does not preserve the order of added data.

#### :bangbang: What is the difference between HashMap and Hashtable :bangbang:

In general HashMap is a newer version of HashTable with some differences:

Hashtable | HashMap
--------- | ----------
thread safe (synchronized) | non thread safe (not synchronized)
slower (allows only operations by one thread at a time) | faster ( multiple threads can operate on it at the same time )
doesn't allow null key nor null values | allows single null key and multiple null values
implements Enumeration interface | implements Iterator interface

#### :bangbang: What is the difference between ArrayList and Vector :bangbang:

We can say that ArrayList is for Vector the same as HashMap is for Hashtable:

Vector | ArrayList
-------- | -------
thread safe (synchronized) | non thread safe (not synchronized)
slower (allows only operations by one thread at a time) | faster ( multiple threads can operate on it at the same time )
implements Enumeration interface | implements Iterator interface

#### :bangbang: What is an immutable object? :bangbang:

* object that can't be modified once created
* any modification of immutable object results in creating new object
* String object is a good example of an immutable object

#### :bangbang: What is the difference between local/instance/class variables? :bangbang:

Local variable:
* defined inside a method
* has to be initialized before it is used (otherwise generates compiler error)
* doesn't have default value

Instance variable:
* defined inside class definition (but outside method definition)
* is created when object is being instantiated
* doesn't have to be initialized (with one exception - when it is declared as `final`)
* is given default value depending of variable type

Class variable:
* defined inside class definition (but outside method definition)
* is being preceded by `static` keyword
* is shared across multiple objects
* doesn't have to be initialized (with one exception - when it is declared as `final`)
* is given default value

Default values of class/instance variables depending on type:

Type | Default value
----- | --------
boolean | false
byte/short/int/long | 0
float/double | 0.0
char | '\u0000' NUL
object | null

#### :bangbang: What are access modifiers? :bangbang:

Access modifiers define the accessibility of a given method or class property for a potential caller.
We have 4 different access modifiers in Java (sorted by their accessibility descending):
* `public` - it is accessible from any class in the program
* `default` ( used by leaving access modifier blank ) - it is accessible only by the class, subclass and any class from the same package
* `protected` - it is accessible from the class and all its subclasses
* `private` - it is accessible only by the main class

#### :bangbang: What is `finalize()` method for? :bangbang:

`finalize()` is a method that can be implemented in any class. Its job is to run additional code just before the destruction of the object.
It can (but not have to) be called before the object is being destroyed. It all depends if the garbage collector tries to collect this object or not.

#### :bangbang: Describe the life cycle of a JSP page :bangbang:

JSP life cycle is similar to the servlet life cycle:

1 Compilation

Every time a request is being send for a particular JSP page,  JSP engine verifies if there is a need to compile this page.
It is necessary if the page was never compiled before or the compiled version of the page is not up to date with the source.

Compilation starts from parsing the JSP page. Each type of data in the page is being translated differently.
As a result we receive new servlet for a given JSP page.

2 Initialization

Before starting to manage the request, JSP engine invokes `jspInit()` method. You can override it to initialize 
any additional resources like database connections.

3 Execution

During this step JSP engine invokes `_jspService()` method which is responsible for managing received request
and returning proper response. 

```java
void _jspService(HttpServletRequest request, HttpServletResponse response)
{
   // Code for handling the request
}
```

4 Finalization

After the servlet has been executed, container invokes the `jspDestroy()` method to remove the servlet from it.
It is possible to override this method to perform any additional cleanup actions.

#### :bangbang: Describe `try` statement :bangbang:

In general its syntax looks like this:

```java
try {
    //some code that might throw an exception
} catch(Exception e) {
    //code executed when exception is thrown
} finally {
    //code executed always 
}
```

* `try` statement is used to catch potential exceptions that might be thrown during the code execution
* if any part of code in `try` block throws an exception, the catch clause tries to catch it
* you can define multiple `catch` clauses that catches different types of exceptions
* always focus on the hierarchy of exceptions in `catch` clauses - they should be written from the most detailed to the most general exception

```java
try {
    throw new FileNotFoundException();
} catch(IOException e) {
     //this block will be executed because FileNotFoundException extends IOException
} catch(FileNotFoundException e) {
     //this block is unreachable
}
```

* `finally` clause is executed every time when the try-catch statement is executed
* at least one of `catch` and `finally` clause is required in every `try` statement (can be both)

#### :bangbang: What is garbage collector and how to initialize it? :bangbang:

* it is a process which looks for objects that became unreachable in the program
* found objects are being removed from the memory heap
* garbage collection is automatic ( Java deals with it by itself )
* it is possible to manually suggest Java to run garbage collector ( use `System.gc()` method )
* you have to be aware that your suggestion may be ignored by the system

