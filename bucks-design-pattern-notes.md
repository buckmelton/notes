# Buck's Design Pattern Notes

## 23 original GoF (Gang of Four) patterns:

Creational:
- Abstract Factory
- Builder
- Factory
- Prototype
- Singleton

Structural:
- Adapter
- Bridge
- Composite
- Decorator
- Facade
- Flyweight
- Proxy

Behavioral:
- Chain of Responsibility
- Command
- Interpreter
- Iterator
- Mediator
- Memento
- Observer
- State
- Strategy
- Template Method
- Visitor

## 14 in Design Patterns in Ruby (Olsen)

### Listing:

Creational:
- Abstract Factory
- Builder
- Factory
- Singleton

Structural:
- Adapter
- Composite
- Decorator
- Proxy

Behavioral:
- Command
- Interpreter
- Iterator
- Observer
- State
- Template Method

### Definitions and Code:

Creational:

#### Abstract Factory

An object dedicated to creating a compatible set of objects.  
The solution is to write a separate class to handle that creation.

![Abstract Factory](images/abstract-factory-pattern.png)
```ruby
class PondOrganismFactory
  def new_animal(name)
    Frog.new(name)
  end

  def new_plant(name)
    Algae.new(name)
  end
end

class JungleOrganismFactory
  def new_animal(name)
    Tiger.new(name)
  end
  def new_plant(name)
    Tree.new(name)
  end
end

class Habitat
  def initialize(number_animals, number_plants, organism_factory)
    @organism_factory = organism_factory
    @animals = []
    number_animals.times do |i|
      animal = @organism_factory.new_animal("Animal#{i}")
      @animals << animal
    end
    @plants = []
    number_plants.times do |i|
      plant = @organism_factory.new_plant("Plant#{i}")
      @plants << plant
    end
  end
  # Rest of the class...
end

jungle = Habitat.new(1, 4, JungleOrganismFactory.new)
jungle.simulate_one_day
pond = Habitat.new( 2, 4, PondOrganismFactory.new)
pond.simulate_one_day

```

Olsen, Russ. Design Patterns in Ruby (Adobe Reader) (Addison-Wesley Professional Ruby Series) (pp. 239-240). Pearson Education. Kindle Edition.

- Builder

### Factory
**Creators**: the base and concrete classes that contain the factory methods (e.g. PizzaStore, NYPizzaStore, ChicagoPizzaStore; Pond, DuckPond, FrogPond)
**Products**: the objects that are being created (Pizza, NYCheesePizza, ChicagoSausagePizza)

You can parameterize the creators' #initialize.
```ruby
class Pond
  def initialize(num_animals, animal_type, num_plants, plant_type)
    ...
  end
end
```

![Factory Pattern](images/factory-pattern.png)

**Example Code**
```ruby
chicagoPizzaStore = ChicagoPizzaStore.new
chicagoPizzaStore.orderPizza("cheese")
# #orderPizza is in PizzaStore and #createPizza is in each of the
# subclassed PizzaStores.  #orderPizza calls #createPizza and there
# is a different #createPizza for each concrete PizzaStore class.
# This is an example of Duck Typing.  We can call #createPizza on
# any class that implements #createPizza.
```
- Singleton

Structural:
- Adapter
- Composite
- Decorator
- Proxy

Behavioral:
#### Command
Encapsulates a request as an object.

Instead of creating a new Button class for every possible thing a Button could do, and having a separate #on_push method for every subclass (OpenDocumentButton#on_push, NewDocumentButton#on_push), create a subclass of Command and assign it dynamically to Button at runtime.

```ruby
class SlickButton

  attr_accessor :command

  def initialize(command)
    @command = command
  end

  #
  # Lots of button drawing and management
  # code omitted...
  #

  def on_button_push
    @command.execute if @command
  end
end

class SaveCommand
  def execute
    #
    # Save the current document...
    #
  end
end

# Associated the appropriate command with the Button when
# the Button is created.
save_button = SlickButton.new(SaveCommand.new)
```
The Command Pattern can also be used to group a bunch of commands together (using a Composite of Commands), Undo commands (for every execute method, implement an unexecute method), and Redo commands.

![Command Pattern](images/command-pattern.png)

![Command Pattern Expanded](images/command-pattern-expanded.png)

#### Interpreter

- Build an Abstract Syntax Tree (AST)
- The AST consists of nodes either TerminalExpression (e.g. LiteralExpression) or NonTerminalExpression (e.g. Sequence-, Alternation-, or RepetitionExpression)
- Start at root of AST and recursively evaluate itself
  - Each node is a subclass of Expression with an #evaluate method that says how to evaluate (also called #interpret or #execute)
- The Context contains information that's global to the interpreter e.g. values of variables in an arithmetic expression.

![Interpreter Pattern](images/interpreter-pattern.png)

- Iterator
#### Observer

The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.



#### Strategy

Context - the user of the Strategy (e.g. "Report")  
Strategy - family of objects that all do the same thing and support the same interface (e.g. superclass Formatter, subclasses HTMLFormatter and PlainTextFormatter, method #output_report)  

![Strategy Pattern](images/strategy-pattern.png)
```ruby
class Report
  def initialize(formatter)
    ...
    @formatter = formatter
  end

  def output_report
    @formatter.output_report(self)  # passing self so formatter can have access to report data
  end
end

report = Report.new(HTMLFormatter.new)
report.output_report
report.formatter = PlainTextFormatter.new
report.output_report
```

### Template Method
The Template Method Pattern defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm’s structure.

![Template Method](images/template-method-pattern.png)

```ruby
class CaffeineBeverage
  def prepare_recipe
    boil_water
    brew
    pour_in_cup
    add_condiments
  end

  # Leave #brew and #add_condiments to subclasses as they
  # differ for Coffee and Tea.

  def boil_water
    # implementation. same for all subclasses
  end

  def pour_in_cup
    # implementation. same for all subclasses
  end
```
