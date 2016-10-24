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

#### Strategy

Context - the user of the Strategy (e.g. "Report")  
Strategy - family of objects that all do the same thing and support the same interface (e.g. superclass Formatter, subclasses HTMLFormatter and PlainTextFormatter, method #output_report)  
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


- Template Method


