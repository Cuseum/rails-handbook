Design patterns are typical solutions to common problems in software design.
Each pattern is like a customizable blueprint used to solve a particular design problem in your code.
They define a language that efficiently improves team communication.

They can also be used to improve code readability, cleanness and simplify the design:

- [Factory](#factory)
  * [Simple factory](#simple-factory)
  * [Factory method](#factory-method)
  * [Abstract factory](#abstract-factory)
- [Special object](#special-object)
  * [Form object](#form-object)
  * [Value object](#value-object)
  * [Null object](#null-object)
  * [Query object](#query-object)
  * [Service object](#service-object)
- [Builder](#builder)
- [Prototype](#prototype)
- [Singleton](#singleton)
- [Adapter](#adapter)
- [Bridge](#bridge)
- [Composite](#composite)
- [Decorator](#decorator)
- [Facade](#facade)
- [Command](#command)
- [State](#state)
- [Strategy](#strategy)
- [Template Method](#template-method)

## Factory
Factory is an ambiguous term that stands for a method or class that supposed to be producing something. Most commonly, factories produce objects. But they may also produce files, records in databases, etc.

### Simple factory
Class that has one creation method with a large conditional.

<details>
  <summary>Problem</summary>
  You have a method which instantiates a different type of object depending on a particular parameter.
</details>

<details>
  <summary>Solution</summary>
  Read more about <a href="https://www.sihui.io/design-pattern-factory/">Simple Factory</a>.
  <br>
  This is considered an intermediate step of introducing <a href="#factory-method">Factory method</a> or <a href="#abstract-factory">Abstract factory</a> patterns.
</details>

### Factory method
Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

<details>
  <summary>Problem</summary>
  Your application contains a <b>Truck</b> class that is used everywhere and now a new <b>Ship</b> class needs to be introduced that will be used in the same places as <b>Truck</b> but with different operations.
</details>

<details>
  <summary>Solution</summary>
  Read more about <b>Factory method</b> <a href="https://refactoring.guru/design-patterns/factory-method">here</a>.
  <br>

  <a href="https://refactoring.guru/design-patterns/factory-method/ruby/example">Ruby example</a>.
  <br>
  If you feel confused about factory comparisons, read more about them <a href="https://refactoring.guru/design-patterns/factory-comparison">here</a>.
</details>


### Abstract factory
One abstraction ladder step higher from the [Factory method](#factory-method) will get you to this design pattern. It lets you produce families of related objects without specifying their concrete classes.

<details>
  <summary>Solution</summary>
  Read more about <b>Abstract factory</b> <a href="https://refactoring.guru/design-patterns/abstract-factory">here</a>.
  <br>
  <a href="https://refactoring.guru/design-patterns/factory-method/ruby/example">Ruby example</a>.
</details>

## Special object

### Form object
Simplify record operations by keeping logic in them.

#### Problem
* Your controllers are huge and you want to make them more readable by extracting some of its logic, but don't want to clutter your models.
* Your opinion is that models shouldn't have validations.
* You have a virtual attribute that works only on a couple of places, but doesn't make sense to add `attr_accessor` to the model.

#### Solution
Read more about *Form object* [here](https://thoughtbot.com/blog/activemodel-form-objects).
_Note_: Form objects work great with [active_type](https://github.com/makandra/active_type).

### Value object
A small simple object, like a date range or location, whose equality isn’t based on identity.

#### Problem
The problem can be spotted by finding:
* attributes that don't make sense on their own
* logic that is tightly coupled with primitives (attributes with behaviour - methods)

#### Solution
Read more about *Value object* [here](https://revs.runtime-revolution.com/value-objects-in-ruby-on-rails-9df64bc8db34).

### Null object
Instead of returning null, or some odd value, return a Special Case that has the same interface as what the caller expects.

#### Problem
You have a lot of conditionals scattered around many classes or view files that ask the same thing. It's usually a low-level error handling part that covers calls to `nil`s.

#### Solution
Read more about *Null object* [here](https://thoughtbot.com/blog/handling-associations-on-null-objects).

### Query object
Represent a database query or a set of database queries related to the same table.

#### Problem
* You want to simplify a class that fetches some data from your database using a complex query
* You want to simplify your model scope to use another class, instead of keeping the query in the caller
* You have a complex SQL query that is used in multiple callers

#### Solution
Read more about *Query object* [here](https://medium.flatstack.com/query-object-in-ruby-on-rails-56ea434365f0).

### Service object
Concentrate the core logic of a request operation into a separate object.

#### Problem
You have a complex set of operations that need to be executed in order synchronously or asynchronously.

#### Solution
Read more about *Service object* [here](http://brewhouse.io/blog/2014/04/30/gourmet-service-objects.html).
_Note_: Service objects can easily become a code smell if not handled properly. If you find yourself with a service object that has too many methods and/or becomes generally unreadable and hard to understand, you might have to find a [bounded context](https://blog.carbonfive.com/bring-clarity-to-your-monolith-with-bounded-contexts/) or use one of the design patterns mentioned in this chapter.

### Builder
Unlike the factories, this design pattern doesn't have a common interface. That makes it possible to different products, using the same construction process.

#### Problem
You have a complex object which goes through many *steps* where you're assigning many fields and relationships. Especially useful for cleaning up classes that have a large amount of method parameters in the constructor that aren't always used.

#### Solution
Read more about *Builder* [here](https://refactoring.guru/design-patterns/builder).

[Ruby example](https://refactoring.guru/design-patterns/builder/ruby/example).

### Prototype
Copy existing objects without making your code dependent on their classes.

#### Problem
You have an ActiveRecord object with lots of relationships that you want to clone.

#### Solution
Read more about *Prototype* [here](https://refactoring.guru/design-patterns/prototype).

[Ruby example](https://refactoring.guru/design-patterns/prototype/ruby/example).
_Note_: The Ruby example uses the usual Marshalling hack to make a deep copy. But it's rather slow and inefficient, therefore, in real applications, use a special gem (eg [deep_cloneable](https://github.com/moiristo/deep_cloneable))

### Singleton
Ensure a class to only have 1 object.

#### Problem
You need a way to only produce the same instance of a class all over your code.

#### Solution
Read more about *Singleton* [here](https://refactoring.guru/design-patterns/singleton).

[Ruby example](https://refactoring.guru/design-patterns/singleton/ruby/example).
_Note_: Singleton has almost the same pros and cons as global variables. Although they’re super-handy, they break the modularity of your code. If you don't care and you're on Rails you can use the *Current* singleton class from `ActiveSupport::CurrentAttributes`.

### Adapter
Allow your incompatible objects to collaborate.

#### Problem
You need a way to transform your ActiveRecord object (or collection) into a valid XML request body.

#### Solution
Read more about *Adapter* [here](https://refactoring.guru/design-patterns/adapter).

[Ruby example](https://refactoring.guru/design-patterns/adapter/ruby/example).

### Bridge
Split a large class or a set of closely related classes into two separate hierarchies

#### Problem
You're planning to add new subclasses which would complicate the class hierarchy.

#### Solution
Transform it into several related hierarchies.
Read more about *Bridge* [here](https://refactoring.guru/design-patterns/bridge).

[Ruby example](https://refactoring.guru/design-patterns/bridge/ruby/example).

### Composite
Compose objects into a tree-like structure and work with the it as if it was a singular object.

#### Problem
You need a way to associate an ActiveRecord object with other ActiveRecord objects of the same class, which in fact may also contain objects of the same class.

#### Solution
Read more about *Composite* [here](https://refactoring.guru/design-patterns/composite).

[Ruby example](https://refactoring.guru/design-patterns/composite/ruby/example).

### Decorator
Add new behaviour to objects by placing them inside special wrapper objects.

#### Problem
You need a method that is using an ActiveRecord object attribute during the operation.
You don't want to add the new method to the model cause it's only used in 1 place.

#### Solution
Read more about *Decorator* [here](https://refactoring.guru/design-patterns/decorator).

[Ruby example](https://refactoring.guru/design-patterns/decorator/ruby/example).
_Note_: The [draper](https://github.com/drapergem/draper) gem does exactly what you want.

### Facade
Provides a well documented, simplified and limited interface to a more complex system.

#### Problem
You want to create an interface with only a couple of public methods that delegate the call to:
* other methods of a gem
* other attributes of an API

#### Solution
Read more about *Facade* [here](https://refactoring.guru/design-patterns/facade).

[Ruby example](https://refactoring.guru/design-patterns/facade/ruby/example).

### Command
Encapsulate your requests as objects which get called using the same interface, thereby giving you more flexibility in object construction.

#### Problem
You have a class that calls different services instantiated with different params depending on a particular parameter.
Easily detectable if you have a `case` statement with calls to services.

#### Solution
Read more about *Command* [here](https://refactoring.guru/design-patterns/command).

[Ruby example](https://refactoring.guru/design-patterns/command/ruby/example).
Another article with a detailed explanation can be [read here](https://www.freecodecamp.org/news/design-patterns-command-and-concierge-in-life-and-ruby-aab9815817ea/).
_Notes_:
* usually combined with the service object pattern
* different from the [Factory method](#factory-method) pattern because the services don't depend on each other and don't share a superclass

### State
Extracts state-related behaviours into separate state classes and forces the original object to delegate the work to an instance of these classes, instead of acting on its own.

#### Problem
You need to convert massive switch-base state machines into objects that the original object calls instead of acting on its own.

#### Solution
Read more about *State* [here](https://refactoring.guru/design-patterns/state).

[Ruby example](https://refactoring.guru/design-patterns/state/ruby/example).

### Strategy
Turn a set of behaviours into objects and make them interchangeable inside the original context object.

#### Problem
Your application requirements changed and now you have to communicate with a 2nd API that returns same type of data as the 1st one.

#### Solution
Read more about *Strategy* [here](https://refactoring.guru/design-patterns/strategy).

[Ruby example](https://refactoring.guru/design-patterns/strategy/ruby/example).

### Template Method
Define a skeleton of an algorithm in a base class and let subclasses override the steps without changing the overall algorithm’s structure.

#### Problem
You have many classes that solve the same semantical issue (importing and data processing from files, JSON/CSV/Excel) and have the same algorithm, but the parsing is different.

#### Solution
Read more about *Template Method* [here](https://refactoring.guru/design-patterns/template-method).

[Ruby example](https://refactoring.guru/design-patterns/template-method/ruby/example).
