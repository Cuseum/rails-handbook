
## Classic design patterns

Design patterns are typical solutions to common problems in software design.
Each pattern is like a customizable blueprint used to solve a particular design problem in your code.
They define a language that efficiently improves team communication.

They can also be used to improve code readability and cleanness, as well as to simplify the design.

[Refactoring.guru](https://refactoring.guru) is a great online place to learn more about them.

## Rails patterns

### Factory
Class that has one creation method with a large conditional.

<details>
  <summary>Problem</summary>
  You have a method which instantiates a different type of object depending on a particular parameter.
</details>

<details>
  <summary>Solution</summary>
  Read more <a href="https://www.sihui.io/design-pattern-factory/" target="_blank" rel="noopener">here</a>.
</details>

### Form object
Simplify record operations by keeping logic in them.

<details>
  <summary>Problem</summary>
  <ul>
    <li>Your controllers are huge and you want to make them more readable by extracting some of their logic, but you don't want to clutter your models.</li>
    <li>Your opinion is that models shouldn't have validations.</li>
    <li>You have a virtual attribute that works only in a couple of places, but it doesn't make sense to add <i>attr_accessor</i> to the model.</li>
  </ul>
</details>

<details>
  <summary>Solution</summary>
  Read more <a href="https://thoughtbot.com/blog/activemodel-form-objects" target="_blank" rel="noopener">here</a>.
  <br>
  <i>Note</i>: Form objects work great with <a href="https://github.com/makandra/active_type" target="_blank" rel="noopener">active_type</a>.
</details>

### Value object
A small simple object, like a date range or location, whose equality isn’t based on identity.

<details>
  <summary>Problem</summary>
  The problem can be spotted by finding:
  <ul>
    <li>attributes that don't make sense on their own</li>
    <li>logic that is tightly coupled with primitives (attributes with behaviour - methods)</li>
  </ul>
</details>

<details>
  <summary>Solution</summary>
  Read more <a href="https://revs.runtime-revolution.com/value-objects-in-ruby-on-rails-9df64bc8db34" target="_blank" rel="noopener">here</a>.
</details>

### Null object
Instead of returning null, or some odd value, return a Special Case that has the same interface as what the caller expects.

<details>
  <summary>Problem</summary>
  You have a lot of conditionals scattered around many classes or view files that check the same thing. It's usually a low-level error handling part that covers calls to <i>nil</i>s.
</details>

<details>
  <summary>Solution</summary>
  Read more <a href="https://thoughtbot.com/blog/handling-associations-on-null-objects" target="_blank" rel="noopener">here</a>.
</details>

### Query object
Represent a database query or a set of database queries related to the same table.

<details>
  <summary>Problem</summary>
  <ul>
    <li>You want to simplify a class that fetches some data from your database using a complex query</li>
    <li>You want to simplify your model scope to use another class, instead of keeping the query in the caller</li>
    <li>You have a complex SQL query that is used in multiple callers</li>
  </ul>
</details>

<details>
  <summary>Solution</summary>
  Read more <a href="https://medium.flatstack.com/query-object-in-ruby-on-rails-56ea434365f0" target="_blank" rel="noopener">here</a>.
</details>

### Service object
Concentrate the core logic of a request operation into a separate object.

<details>
  <summary>Problem</summary>
  You have a complex set of operations that need to be executed in a sequence synchronously or asynchronously.
</details>

<details>
  <summary>Solution</summary>
  Read more <a href="http://brewhouse.io/blog/2014/04/30/gourmet-service-objects.html" target="_blank" rel="noopener">here</a>.
  <br>
  <i>Note</i>: Service objects can easily become a code smell if not handled properly. If you find yourself with a service object that has too many methods and/or becomes generally unreadable and hard to understand, you might have to find a <a href="https://blog.carbonfive.com/bring-clarity-to-your-monolith-with-bounded-contexts/" target="_blank" rel="noopener">bounded context</a> or use one of the design patterns mentioned in this chapter.
</details>
