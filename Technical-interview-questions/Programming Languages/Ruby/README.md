# Ruby Interview questions

## 1. What is Ruby, and what are its key features?
Answer: Ruby is a dynamic, object-oriented programming language known for its simplicity and productivity. 
#### Key features include:
- Object-oriented: Everything in Ruby is an object.
- Dynamic typing: Variable types are determined at runtime.
- Garbage collection: Automatic memory management.
- Expressive syntax: Designed to be natural to read and easy to write.

## 2. How do you define a class in Ruby?
Answer: A class in Ruby is defined using the class keyword. Here’s an example:


```ruby
class Animal
  def speak
    "Roar!"
  end
end

lion = Animal.new
puts lion.speak  # Output: Roar!
```

## 3. What are blocks, procs, and lambdas in Ruby?
Answer:
Blocks: Anonymous pieces of code that can accept parameters and be passed to methods.
Procs: Objects that encapsulate blocks and can be stored in variables.
Lambdas: Similar to procs but with stricter argument checking and return behavior.

#### Example:


```ruby
# Block
def greet
  yield("World")
end

greet { |name| puts "Hello, #{name}!" }  # Output: Hello, World!

# Proc
my_proc = Proc.new { |name| puts "Hello, #{name}!" }
my_proc.call("Alice")  # Output: Hello, Alice!

# Lambda
my_lambda = ->(name) { puts "Hello, #{name}!" }
my_lambda.call("Bob")  # Output: Hello, Bob!
```

## 4. What is the difference between == and === in Ruby?
Answer:
== checks for value equality, i.e., whether two objects have the same value.
=== is used for case equality, often in case statements and can be overridden in classes.


#### Example:


```ruby
# Using ==
puts (5 == 5)  
# Output: true
puts (5 == "5")  
# Output: false

# Using ===
class MyClass
  def self.=== (other)
    other.is_a?(String)
  end
end

puts MyClass === "Hello"  
# Output: true
puts MyClass === 5        
# Output: false
```


## 5. Explain how to handle exceptions in Ruby.
Answer: Exceptions in Ruby can be handled using begin, rescue, and ensure blocks.

#### Example:

```ruby
begin
  puts 10 / 0
rescue ZeroDivisionError
  puts "You can't divide by zero!"
ensure
  puts "This will always run."
end

# Output:
# You can't divide by zero!
# This will always run.
```

## 6. What is a mixin, and how is it used in Ruby?
Answer: A mixin is a module that can be included in classes to add functionality. It allows for sharing methods across classes without using inheritance.

#### Example:


```ruby
module Walkable
  def walk
    "Walking..."
  end
end

class Person
  include Walkable
end

class Dog
  include Walkable
end

person = Person.new
dog = Dog.new

puts person.walk  # Output: Walking...
puts dog.walk     # Output: Walking...
```

## 7. What are instance variables and class variables in Ruby?
Answer:
Instance Variables: Variables that belong to a specific instance of a class, prefixed with @.
Class Variables: Variables shared among all instances of a class, prefixed with @@.


#### Example:

```ruby
class Example
  @@class_variable = 0

  def initialize(value)
    @instance_variable = value
  end

  def show_variables
    puts "Instance Variable: #{@instance_variable}"
    puts "Class Variable: #{@@class_variable}"
  end
end

obj = Example.new(42)
obj.show_variables
# Output:
# Instance Variable: 42
# Class Variable: 0
```

## 8. How do you create a simple Ruby gem?
Answer: To create a simple Ruby gem, you can follow these steps:
Create a directory for your gem.
Create a gemspec file.
Write your code.
Build and install the gem.


#### Example:


```bash
# Step 1: Create directory
mkdir my_gem
cd my_gem

# Step 2: Create gemspec file (my_gem.gemspec)
# my_gem.gemspec
Gem::Specification.new do |spec|
  spec.name        = 'my_gem'
  spec.version     = '0.1.0'
  spec.summary     = 'A simple example gem'
  spec.files       = Dir['lib/**/*.rb']
end

# Step 3: Write your code (lib/my_gem.rb)
# lib/my_gem.rb
module MyGem
  def self.hello
    "Hello from MyGem!"
  end
end

# Step 4: Build the gem
gem build my_gem.gemspec

# Step 5: Install the gem
gem install my_gem-0.1.0.gem
```

## 9. What is the purpose of self in Ruby?
Answer: In Ruby, self refers to the current object and can be used:
To define class methods.
To refer to instance variables within a class.

#### Example:

```ruby
class Example
  def self.class_method
    puts "This is a class method."
  end

  def instance_method
    puts "This is an instance method."
  end
end

Example.class_method  # Output: This is a class method.
obj = Example.new
obj.instance_method    # Output: This is an instance method.
```

## 10. How do you iterate over a collection in Ruby?
Answer: You can iterate over collections using methods like each, map, and select.

#### Example:

```ruby
numbers = [1, 2, 3, 4, 5]

# Using each
numbers.each do |number|
  puts number * 2
end

# Using map
doubled = numbers.map { |number| number * 2 }
puts doubled.inspect  # Output: [2, 4, 6, 8, 10]

# Using select
evens = numbers.select { |number| number.even? }
puts evens.inspect  # Output: [2, 4]
```