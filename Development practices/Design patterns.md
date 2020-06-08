Design patterns are typical solutions to common problems in software design.
Each pattern is like a customizable blueprint used to solve a particular design problem in your code.
They define a language that efficiently improves team communication.

They can also be used to improve code readability, cleanness and simplify the design.

## Factory
Factory is an ambiguous term that stands for a method or class that supposed to be producing something. Most commonly, factories produce objects. But they may also produce files, records in databases, etc.

### Simple Factory
Class that has one creation method with a large conditional.

#### Problem
You have a method which instantiates a different type of object depending on a particular parameter.

#### Solution
```ruby
class UserFactory
  def self.build(type)
    case type
    when 'user'
      User.new
    when 'admin'
      Admin.new
    when 'staff'
      Employee.new
    else
      raise "unsupported type(#{type}) passed to #{self.name}"
    end
  end
end
```

This is considered an intermediate step of introducing Factory Method or Abstract Factory patterns.

### Factory Method
Provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

#### Problem
Your application contains a `Truck` class that is used everywhere and now a new `Ship` class needs to be introduced that will be used in the same places as `Truck` but with different operations.

#### Solution
```ruby
class Vehicle
  def package
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end

  def deliver
    package.deliver
  end
end

class Truck < Vehicle
  def package
    Livestock.new
  end
end

class Ship < Vehicle
  def package
    HeavyCargo.new
  end
end

class Package
  def deliver
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end
end

class Livestock < Package
  def deliver
    # livestock delivery logic
  end
end

class HeavyCargo < Package
  def deliver
    # heavy cargo delivery logic
  end
end
```

You can combine the Simple Factory with the Factory Method to get:
```ruby
class DeliveriesController
  def create
    @delivery = VehicleFactory.new(params[:vehicle]).deliver
  end
end
```

Read more about *Factory Method* [here](https://refactoring.guru/design-patterns/factory-method).
[Ruby example](https://refactoring.guru/design-patterns/factory-method/ruby/example).

If you feel confused about factory comparisons, read more about them [here](https://refactoring.guru/design-patterns/factory-comparison).

### Abstract Factory
One abstraction ladder step higher from the Factory Method will get you to this design pattern. It lets you produce families of related objects without specifying their concrete classes.

Read more about *Abstract Factory* [here](produce families of related objects without specifying their concrete classes).
[Ruby example](https://refactoring.guru/design-patterns/factory-method/ruby/example).

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
