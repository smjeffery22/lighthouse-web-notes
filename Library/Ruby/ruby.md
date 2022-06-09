# RUBY

## RUBY STYLE GUIDE

  - `snake_case` for symbols, methods and variables
    - also for files and directories
    ```ruby
    # bad
    :'some symbol'
    :SomeSymbol
    :someSymbol

    someVar = 5

    def someMethod
      # some code
    end

    def SomeMethod
      # some code
    end

    # good
    :some_symbol

    some_var = 5

    def some_method
      # some code
    end
    ```
    
  - `CapitalCase` for Classes and Modules
    - One class/module per source file
    - Name the file name as the class/module
      - replace Capital_Case with snake_case
    ```ruby
    # bad
    class Someclass
      # some code
    end

    class Some_Class
      # some code
    end

    # good
    class SomeClass
      # some code
    end
    ```

  - `SCREAMING_SNAKE_CASE` for constants
    ```ruby
    # bad
    SomeConst = 5

    # good
    SOME_CONST = 5
    ```

  - `End in a question mark` for methods that return a boolean value
    - not for methods that do not return a boolean
    ```ruby
    # bad
    def even(value)
    end

    # good
    def even?(value)
    end
    ```

  - `%w` to the literal array syntax to create an *array of words* with two or more elements
    ```ruby
    # bad
    STATES = ['draft', 'open', 'closed']

    # good
    STATES = %w[draft open closed]
    ```

    - `%i` to the literal array syntax to create an *array of symbols* with two or more elements
    ```ruby
    # bad
    STATES = [:draft, :open, :closed]

    # good
    STATES = %i[draft open closed]
    ```

  - Prefer *symbols* instead of strings as hash keys
    ```ruby
    # bad
    hash = { 'one' => 1, 'two' => 2, 'three' => 3 }
    hash = { one: one, two: two, three: three }

    # good
    hash = { one: 1, two: 2, three: 3 }
    hash = { one:, two:, three: }
    ```

  - Hash #key #each #fetch
    ```ruby
    ####key####
    # bad
    hash.has_key?(:test)
    hash.has_value?(value)

    # good
    hash.key?(:test)
    hash.value?(value)

    ####each####
    # bad
    hash.keys.each { |k| p k }
    hash.values.each { |v| p v }
    hash.each { |k, _v| p k }
    hash.each { |_k, v| p v }

    # good
    hash.each_key { |k| p k }
    hash.each_value { |v| p v }

    ####fetch####
    heroes = { batman: 'Bruce Wayne', superman: 'Clark Kent' }
    # bad - if we make a mistake we might not spot it right away
    heroes[:batman] # => 'Bruce Wayne'
    heroes[:supermann] # => nil

    # good - fetch raises a KeyError making the problem obvious
    heroes.fetch(:supermann)
    ```

  - Prefer map over 
    - collect, find over
      - detect, select over
        - find_all, reduce over
          - inject, include? over
            - member? and size over
              - length. 

  - Underscore large numeric literals
    ```ruby
    # bad - how many 0s are there?
    num = 1000000

    # good - much easier to parse for the human brain
    num = 1_000_000
    ```

  
## RUBY VERSION MANAGEMENT (RVM)

```
// check Ruby version
ruby -v
ruby --version

// check currently install Ruby versions
rvm
rvm ls
```

## irb - THE RUBY SHELL

  - Similar to Node CLI, `irb` command can be used to launch a REPL

```ruby
#irb
puts "Hello, what's your name?" // asks for input - name
name = gets.chomp // user-input
puts "Welcome to \"Ruby land\", #{name}. Hope you enjoy your stay (and never leave!)" // prints with name assigned
```

## GEMS (PACKAGES)

  - 3rd party libraries similar to npm
    - i.e. Rails

```
gem
gem list
```

## FUNCTIONS

  - Functions can be created using `def` (define)

```ruby
def print_two_again(arg1, arg2)
  puts "arg1: #{arg1}, arg2: #{arg2}"
end

print_two_again("Bori", "Park")
```

## IFs

  - `elsif` instead of `else if`

```ruby
if people < cats
  puts "Too many cats! The world is doomed!"
end

###############################################################################################


if cars > people
  puts "We should take the cars."
elsif cars < people
  puts "We should not take the cars"
else
  puts "We can't decide"
end

###############################################################################################

puts "You enter a dark room with two doors. Do you go through door #1 or door #2?"

print "> "
door = $stdin.gets.chomp

if door == "1"
  puts "There is a giant bear here eating a cheese cake. What do you do?"
  puts "1. Take the cake."
  puts "2. Scream at the bear."

  print "> "
  bear = $stdin.gets.chomp

  if bear == "1"
    puts "The bear eats your faceoff. Good job!"
  elsif bear == "2"
    puts "The bear eats your legs off. Good job!"
  else
    puts "Well, doing %s is probably better. Bear runs away." % bear
  end

elsif door == "2"
  puts "You stare into the endless abyss at Cthulhu's retina."
  puts "1. Blueberries"
  puts "2. Yellow jacket clothespins"
  puts "3. Understanding revolvers yelling melodies"

  print "> "
  insanity = $stdin.gets.chomp

  if insanity == "1" || insanity == "2"
    puts "Your body survives powered by a mind of jello. Good job!"
  else
    puts "The insanity rots your eyes into a pool of muck. GJ!"
  end

else
  puts "You stumble around and fall on a knife and die. Good job!"
end
```

## FOR LOOPS

  - Use `.each` to loop over

```ruby
the_count = [1, 2, 3, 4, 5]
fruits = ['apples', 'oranges', 'pears', 'apricots']
change = [1, 'pennies', 2, 'dimes', 3, 'quarters']

for number in the_count
  puts "This is count #{number}"
end

fruits.each do |fruit|
  puts "A fruit of type: #{fruit}"
end

change.each { |i| puts "I got #{i}" }

elements = []

(0..5).each do |i|
  puts "adding #{i} to the list"
  elements.push(i)
end

puts elements.inspect

elements.each { |i| puts "Element was: #{i}" }
```

## YIELD

  - In Ruby, a *block* is a chunk of code that can be passed to and executed by any method
    - a piece of code enclosed by *{} or do*
  - *Block are always used with methods*, which usually feed data to them (as arguments)
  - Each time a call is made to *yield*, the code in the `do block` or inside `{}` will be ran
  - *Any method can receive a block as an implicit argument*
    - a block is executed by the yield statement within a method
  - Each method can *receive only one block*

  - If a method contains a yield statement, it is expecting to receive a block at calling time
    - if block is not provided, error *LocalJumpError: no block given (yield)*
    - block can be optional by using `block_given?`

```ruby
def meditate
  print "Today we will practice zazen"
  yield # This indicates the method is expecting a block
end 

# We are passing a block as an argument to the meditate method
meditate { print " for 40 minutes." }

Output:
Today we will practice zazen for 40 minutes.

def meditate
  puts "Today we will practice zazen."
  yield if block_given? 
end meditate

Output:
Today we will practice zazen. 
```

```ruby
def test
  yield 5
  puts "You are in the method test"
  yield 100
end

test {|i| puts "You are in the block #{i}"}

test do |i|
    puts "You are in the block #{i}"
end

# You are in the block 5
# You are in the method test
# You are in the block 100
# You are in the block 5
# You are in the method test
# You are in the block 100
```

## CLOSURES

  - A closure piece of code that can be passed around
    - *Blocks* and *Procs*

## CONSTANTS AND NAESPACE

  - In Ruby, any keyword with a *capitalized first letter* is considered a *constant*
  - *Constant* can refer to a Module, Class or simple data like Floats and Strings
  - `::` syntax used to access constants
  - 
  ```ruby
  # in irb:
  #   apple => NameError: undefined local variable or method `apple' for main:Object
  #   Apple => NameError: uninitialized constant Apple
  ```

```ruby
Math::PI # => 3.141592653589793
Math.class # => Module
Math::PI.class # => Float
```

  - PI is a *constant*
  - Math is also a *constant* that refers to a *Module*
  - PI constant within the Math *space*
  - To refer to PI from outside of the Math *namespace*
    - Must be explicit and use *Math::PI*
  - Both *Module and Class constants* create a *namespace* within which other constants can be placed

### NAMESPACE

  - A set of signs (names) used to *identify* and *refer* to *objects* of various kinds
  - Ensures that all of a *given set of objects have unique names* so that they can be easily identified
    - Allow reuse of names in different contexts
  - To group symbols and identifiers to avoid name collisions

  ```ruby
  gem money
  require "money"
  Money # => does not throw error after installing it

  Money.constants # => returns an array with Modules within Money class
  # => [:Currency, :Bank, :RatesStore, :Arithmetic, :Constructors, :FormattingRules, :Formatter, :Allocation, :LocaleBackend, :UndefinedSmallestDenomination, :CoercedNumeric] 

  Money::Bank.class # => Module

  Money::Bank.constants # => returns an array with Classes within Bank Module
  # => [:Error, :UnknownRate, :Base, :UnknownRateFormat, :VariableExchange, :DifferentCurrencyError, :SingleCurrency] 
  ```

## OBJECT ORIENTED PROGRAMMING (OOP)

  - A programming paradigm that was created to deal with the growing complexity of large software systems

### ENCAPSULATION

  - Hiding pieces of functinality and making it unavailable to the rest of the code base
  - A form of data protection
    - Data cannot be manipulated or changed 
    - Ruby achieves this by creating objects

### POLYMORPHISM

  - Ability for different types of data to respond to a common interface

### INHERITANCE

  - Where a class inherits the behaviours of another class, referred to as the *superclass*
  - Define basic classes with large reusability
    - Smaller *subclasses* for more fine-grained, detailed behaviours

  
### OBJECTS

  - Anything that can be said to have a value is an object
    - Numbers
    - Strings
    - Arrays
    - Classes
    - Modules
  - Non-objects:
    - Methods
    - Blocks
    - Variables
  
  - Objects are created from classes
    - Each object contains *different information*
    - However, they are *instances of the same class*
    
    ```ruby
    "hello".class # => String
    "world".class # => String
    ```
      - "hello" and "world" are objects
      - instantiated from a String class

  - **Creating an Object**
    1. Create a Class
    2. Instantiate the Class with `.new` method
    3. Save it in a variable => object

### CLASSES

  - A class can be defiend using `class`
  - *CamelCase* naming convention to create the name
  - `end` to finish the definition
  - File name should be in *snake_case* and reflect the class name

    ```ruby
    #good_dog.rb
    class GoodDog
    end

    sparky = GoodDog.new
    ```
      - *Instance* of GoodDog class created and stored in the variable `sparky`
        - Instantiating GoodDog class by using the `.new` method
      - `sparky` is an *object* or *instance* of class `GoodDog`

    !["GoodDog Class"](https://d2aw5xe2jldque.cloudfront.net/books/ruby/images/class_instance_diagram.jpg)

### MODULES

  - Collection of behaviours that is usable in other classes via *mixins*
    - Allows to group reusable codes into one place
    - Modules also used as a *namespace*
  - Cannot create an object with a module
  - Must be mixed in with a class using the *include* method invocation (*mixin*)
    - After mixing in a module, the behaviours declared in that module are available to the class and its objects

  - **Purposes**
    1. Extend the functionality
    2. Namespacing => organize code

  ```ruby
  # Extend the functionality
  module Speak
    def speak(sound)
      puts sound
    end
  end

  class GoodDog
    include Speak
  end

  class HumanBeing
    include Speak
  end

  sparky = GoodDog.new
  sparky.speak("Arf!") # => Arf!
  bob = HumanBeing.new
  bob.cpeak("Hello") # => Hello!
  ```
    - *Objects:* `sparky` and `bob`
    - *Method:* `speak`
    - *Module:* `Speak`
      - "Mixing in" the module Speak

```ruby
# Namespacing
module Careers
  class Engineer
  end

  class Teacher
  end
end

first_job = Careers::Teacher.new
```

### METHOD LOOKUP

 - `.ancestors` method on any class to find out the method lookup chain

```ruby

module Speak
  def speak(sound)
    puts "#{sound}"
  end
end

class GoodDog
  include Speak
end

class HumanBeing
  include Speak
end

puts "---GoodDog ancestors---"
puts GoodDog.ancestors
puts ''
puts "---HumanBeing ancestors---"
puts HumanBeing.ancestors
```

```ruby
---GoodDog ancestors---
GoodDog
Speak
Object
Kernel
BasicObject

---HumanBeing ancestors---
HumanBeing
Speak
Object
Kernel
BasicObject
```

  - `Speak` module placed between the `custom classes` (i.e. GoodDog and HumanBeing) and the `Object` class that comes with Ruby
  - Since `speak` method is not defined in the `GoodDog` class, the next place it looks is the `Speak` module

## CLASSES AND OBJECTS - PART 1

### STATES AND BEHAVIOURS

  - *States* track *attributes* for individual objects
  - *Behaviours* are *what objects are capable of doing*

  - *Instance variables* keep track of state
    - Ex. information contained in objects (i.e. name, weight, height)
  - *Instance methods* expose behaviour for objects
    - Ex. methods defined in a class that are avilable to objects of that class

### INITIALIZING A NEW OBJECT

  ```ruby
  class GoodDog
    def initialize
      puts "This object was initialized!"
    end
  end

  sparky = GoodDog.new        # => "This object was initialized!"
  ```

  - `initialize` method gets called every time a new object is created
  - `initialize` method is a *constructor*

### INSTANCE VARIABLES

  ```ruby
  class GoodDog
    def initialize(name)
      @name = name
    end
  end

  sparky = GoodDog.new("Sparky")
  ```

  - A variable with `@` symbol in front is called an *instance variable*
    - Variable that exists as long as the object instance exists
      Responsible for *keeping track of information* about the *state* of an object
  - Arguments can be passed through the `.new` method
    - Assigned to the local variable *name*
    - Set the instance variable *@name* to *name*

### INSTANCE METHODS

  ```ruby
  class GoodDog
    def initialize(name)
      @name = name
    end

    def speak
      "Arf!"
    end

    def speak_name
      "#{@name} says arf!"
    end

    # def get_name
    def name
      @name
    end

    # def set_name=(name)
    def name=(n)
      @name = n
    end
  end

  sparky = GoodDog.new("Sparky")
  puts sparky.speak               # => Arf!
  puts sparky.speak_name          # => Sparky says arf!
  puts sparky.get_name            # => Sparky
  sparky.set_name="Spartacus"   # => changes sparky's name
  puts sparky.get_name            # => Spartacus

  fido = GoodDog.new("Fido")
  puts fido.speak                 # => Arf!
  ```

  - Both objects (sparky and fido) can perform the same behaviours
    - *All objects* of the *same class* have the *same behaviours*
  - Two objects contain *different states* (i.e. name)

### ACCESSOR METHODS

  - **getter method**
    - `sparky.name` does not return the name
      - `NoMethodError: undefined method 'name' for #<GoodDog:0x007f91821239d0 @name="Sparky">`
        - Means that non-existence method was called
    - `get_name` instance method can be added to return @name

  - **setter method**
    - To change sparky's name
    - `set_name=` instance method allows to change the name
      - Ruby gives a special syntax for setter methods
        - `sparky.name = "Spartacus"` instead of `sparky.set_name=("Spartacus")`
  
  - Ruby's convention is to name *getter and setter methods* using the *same name as the instance variable*

  - **attr-accessor**
    - Takes a *symbol as an argument*, which it uses to *create the method name* for the *getter and setter* methods
    - *attr_reader* for only getter method
    - *attr-writer* for only setter method
    - *Variables* inside initialize method are *local* and not accessible (i.e. private method)

    ```ruby
    class GoodDog
      attr_accessor :name

      def initialize(name)
        @name = name
      end

      def speak
        "#{@name} says arf!"
      end
    end

    sparky = GoodDog.new("Sparky")
    puts sparky.speak
    puts sparky.name            # => "Sparky"
    sparky.name = "Spartacus"
    puts sparky.name            # => "Spartacus"
    ```

#### ACCESSOR METHOD WITHIN CLASS

**getter**

  ```ruby
  def speak
    "#{@name} says arf!"
  end

  # use getter method insead to call the name
  def speak
    "#{name} says arf!"
  end
  ```

  ```ruby
  # converts '123-45-6789' to 'xxx-xx-6789'
  # calling ssn directly through getter method
  'xxx-xx-' + @ssn.split('-').last

  # manipulate ssn using instance method then call it
  # ssn will always start with 'xxx-xx-'
  def ssn
    # converts '123-45-6789' to 'xxx-xx-6789'
    'xxx-xx-' + @ssn.split('-').last
  end
  ```

**setter**

**self**
  - `self.` tells Ruby that we are *calling a method*
    - `@` directly accesses instance variable
    - Below will use getter method instead of @name (first code)
    - If there was another method called name, self. would call that method (second code)

  ```ruby
  class GoodDog
    attr_accessor :name, :height, :weight

    def initialize(n, w, h)
      @name = n
      @weight = w
      @height = h
    end
  end

  # grab instance variables from the constructor (i.e. initialize)
  def change_info(n, h, w)
    @name = n
    @height = h
    @weight = w
  end

  # to tell Ruby to call method (i.e. setter method)
  def change_info(n, h, w)
    self.name = n
    self.height = h
    self.weight = w
  end

  def info
    "#{self.name} weighs #{self.weight} and is #{self.height} tall."
  end
  ```

  ```ruby
  class GoodDog
    attr_accessor :name, :height, :weight

    def initialize(n, w, h)
      @name = n
      @weight = w
      @height = h
    end

    def name
      puts "name was called"
      @name
    end
  end

  # to tell Ruby to call method (i.e. name method)
  def change_info(n, h, w)
    self.name = n
    self.height = h
    self.weight = w
  end

  def info
    "#{self.name} weighs #{self.weight} and is #{self.height} tall."
  end
  ```

## CLASSES AND OBJECTS - PART 2

### CLASS METHODS

  - Class level methods - **class methods**
    - Method that can be used directly on the class itself
      - Without having to instantiate any objects
  - *Prepend the method name with `self.`*
  
  ```ruby
  class GoodDog
    def self.what_am_i
      puts "I'm a GoodDog class"
    end
  end

  GoodDog.what_am_i       # => I'm a GoodDog class
  ```

### CLASS VARIABLES

  - Variables for an entire class - **class variables**
  - Created using `@@`
  - Counter initialized in initialize method

  ```ruby
  class GoodDog
    @@number_of_dogs = 0
    
    def initialize
      @@number_of_dogs += 1
    end

    def self.total_number_of_dogs
      @@number_of_dogs
    end
  end

  puts GoodDog.total_number_of_dogs   # => 0

  dog1 = GoodDog.new
  dog2 = GoodDog.new

  puts GoodDog.total_number_of_dogs   # => 2
  ```
  
  - Every time an object is instantiated using GoodDog class, the constructor (initialize method) get called
    - Increments number_of_dogs

### CONSTANTS

  - Constants can be defined using an upper case letter at the beginning of the variable name
    - Usually ALL CAPS

  ```ruby
  class GoodDog
    DOG_YEARS = 7

    attr_accessor :name, :age

    def initialize(n, a)
      self.name = n
      self.age  = a * DOG_YEARS
    end
  end

  sparky = GoodDog.new("Sparky", 4)
  puts sparky.age             # => 28
  ```

### THE TO_S METHOD

  - `to_s` instance method comes *built in to every class* in Ruby
  - `puts sparky` => #<GoodDog:0x007fe542323320>
    - puts method automatically calls to_s on its argument
      - equivalent to `puts sparky.to_s`
    - to_s returns the *name of the object's class* and an *encoding of the object id*
  
  ```ruby
  class GoodDog
    DOG_YEARS = 7

    attr_accessor :name, :age

    def initialize(n, a)
      @name = n
      @age  = a * DOG_YEARS
    end

    def to_s
      "This dog's name is #{name} and it is #{age} in dog years."
    end
  end

  puts sparky      # => This dog's name is Sparky and is 28 in dog years.
  ```

  - Since to_s is automatically added to puts, creating a method called to_s automatically appends it when puts sparky is called
    - Calls the instance method instead of default to_s (object's class name and encoding)

### P (A.K.A INSPECT)

  - Similar to puts, except it does not call to_s on its argument
    - Calls another built-in Ruby instance method called `inspect`
  - `p sparky` <=> `puts sparky.inspect`
    - #<GoodDog:0x007fe54229b358 @name="Sparky", @age=28>

### MORE ON SELF

**self inside of an instance method**

  ```ruby
  class GoodDog
    attr_accessor :name, :height, :weight

    def initialize(n, h, w)
      self.name   = n
      self.height = h
      self.weight = w
    end

    def what_is_self
      self
    end
  end

  sparky = GoodDog.new('Sparky', '12 inches', '10 lbs')
  p sparky
  # => #<GoodDog:0x007f83ac062b38 @name="Sparky", @height="12 inches", @weight="10 lbs">

  p sparky.what_is_self
  # => #<GoodDog:0x007f83ac062b38 @name="Sparky", @height="12 inches", @weight="10 lbs">
  ```

  - `self` references the *calling object* if used inside of an instance method

**self inside of an instance method**

  ```ruby
  class GoodDog
    # ... rest of code omitted for brevity
    puts self
  end

  GoodDog     # => GoodDog
  ```

  - self inside a class but outside an instance method refers to the class itself

#### SELF RULES

  1. self, inside of an instance method:
      - References the instance (object) that called the method - the calling object
      - Therefore, self.weight= is the same as sparky.weight=, in above examples

  2. self, outside of an instance method:
      - References the class and can be used to define class methods
      - Therefore, if we were to define a name class method, def self.name=(n) is the same as def GoodDog.name=(n)

## INHERITANCE

  - *Inheritance* is when a class *inherits behaviour* from another class
    - *Superclass* class that inherits behaviour down to *subclass*
  - To extract *common behaviour* from classes that share that behaviour, and move it *to a superclass*

  ```ruby
  class Animal
    def speak
      "Hello!"
    end
  end

  class GoodDog < Animal
  end

  class Cat < Animal
  end

  sparky = GoodDog.new
  paws = Cat.new
  puts sparky.speak           # => Hello!
  puts paws.speak             # => Hello!
  ```

  - `speak` method is being extracted to a superclass Animal
    - inheritance to make this behaviour available to other classes (i.e. subclasses)
  - `<` symbol to signift that GoodDog and Cat classes are inheriting from the Animal class
  - Ruby checks the object's class first for the method before looking in the superclass
    - if speak method was defined within GoodDog class, sparky.speak would call the speak method within GoodDog class, not from superclass

### SUPER

  - `super` keyword is called within a method to search for a method with the same name from the superclass
  - Also commonly used with `initialize` method
    - arguments passed to subclass method first then to superclass

  ```ruby
  class Animal
    def speak
      "Hello!"
    end
  end

  class GoodDog < Animal
    def speak
      super + " from GoodDog class"
    end
  end

  sparky = GoodDog.new
  sparky.speak        # => "Hello! from GoodDog class"
  ```

  ```ruby
  class Animal
    attr_accessor :name

    def initialize(name)
      @name = name
    end
  end

  class GoodDog < Animal
    def initialize(color, name)
      super(name)
      @color = color
    end
  end

  bruno = GoodDog.new("bori", "brown")        # => #<GoodDog:0x007fb40b1e6718 @color="brown", @name="brown">
  ```

### MODULES

  - Modules can be created and used in classes (i.e. mixins)
    - Instead of class-to-class inheritance, inherits the interface provided by the mixin module
      - *interface inheritance*
  - Common naming convention in Ruby to use the *"-able" suffix* on whatever verb describes the behaviour that the module is modelling
    - i.e. Swimm`able`

  ```ruby
  module Swimmable
    def swim
      "I'm swimming!"
    end
  end

  class Animal; end

  class Fish < Animal
    include Swimmable         # mixing in Swimmable module
  end

  class Mammal < Animal
  end

  class Cat < Mammal
  end

  class Dog < Mammal
    include Swimmable         # mixing in Swimmable module
  end

  sparky = Dog.new
  neemo  = Fish.new
  paws   = Cat.new

  sparky.swim                 # => I'm swimming!
  neemo.swim                  # => I'm swimming!
  paws.swim                   # => NoMethodError: undefined method `swim' for #<Cat:0x007fc453152308>
  ```

### INHERITANCE VS. MODULES

**Class Inheritance**
  - *subclass* can only be inherited *frmo one class*
  - *is-a* relationship
    - i.e. dog "is-an" animal
  

**Interface Inheritance**
  - can *mix as many modules* as one would like
  - *has-a* relationship
    - i.e. dog "has an" ability to swim
  - Modules cannot be instantiated (i.e. no object can be created frmo a module)
    - Used only for namespacing and grouping common methods together
  - `.ancestor` class method can be used to look up method path

### METHOD LOOKUP PATH

  - Path that Ruby takes to look for a method

  ```ruby
  module Walkable
    def walk
      "I'm walking."
    end
  end

  module Swimmable
    def swim
      "I'm swimming."
    end
  end

  module Climbable
    def climb
      "I'm climbing."
    end
  end

  class Animal
    include Walkable

    def speak
      "I'm an animal, and I speak!"
    end
  end

  class GoodDog < Animal
    include Swimmable
    include Climbable
  end

  puts "---Animal method lookup---"
  puts Animal.ancestors

  #---Animal method lookup---
  # Animal
  # Walkable
  # Object
  # Kernel
  # BasicObject

  puts "---GoodDog method lookup---"
  puts GoodDog.ancestors

  #---GoodDog method lookup---
  # GoodDog
  # Climbable
  # Swimmable
  # Animal
  # Walkable
  # Object
  # Kernel
  # BasicObject
  ```

  - Method lookup path lists the *last module included in the class first*
  - Superclass and its module are also included in the path
    - All GoodDog objects will have access to both its modules and the module from Animal class
    - Modules included in the class comes up in the list before the superclass

### MODULES FOR NAMESPACING

  - Organizing similar classes under a module
    - Group related classes under a module
    - Easy to recognize related classes in the code
    - Avoid classes colliding with other similarly named classes
  - Classes in a module can be called by using `::`
  
  ```ruby
  module Mammal
    class Dog
      def speak(sound)
        p "#{sound}"
      end
    end

    class Cat
      def say_name(name)
        p "#{name}"
      end
    end
  end

  buddy = Mammal::Dog.new
  kitty = Mammal::Cat.new
  buddy.speak('Arf!')           # => "Arf!"
  kitty.say_name('kitty')       # => "kitty"
  ```

### MODULES AS A CONTAINER METHODS (MODULE METHODS)

  - Using modules to house other methods

  ```ruby
  module Mammal
    ...

    def self.some_out_of_place_method(num)
      num ** 2
    end
  end

  value = Mammal.some_out_of_place_method(4)      # => 4 (preferred way)
  value = Mammal::some_out_of_place_method(4)     # => 4
  ```

### ACCESS CONTROL

  - Generally implemented through the use of *access modifiers*
    - To allow or restrict access to a particular thing
  - In Ruby, concerned with restricting access to methods defined in a class
    - *Method Access Control*
  - *Method Access Control* implemented through the use of the following access modifiers:
    
    - *public* method is available to anyone who knows either the class name or the object's name
      - available to the rest of the program
    
    - *private* method does the work in the class but do not need to be available to the rest of the program
      - Use `private` method and anything below it becomes private method
      - *Only accessible from other methods in the class without self.*

      ```ruby
      class GoodDog
        DOG_YEARS = 7

        attr_accessor :name, :age

        def initialize(n, a)
          self.name = n
          self.age = a
        end

        def public_disclosure
          "#{self.name} in human years is #{human_years}"
        end

        private

        def human_years
          age * DOG_YEARS
        end
      end

      sparky = GoodDog.new("Sparky", 4)
      sparky.human_years                  # => NoMethodError: private method `human_years' called for ...
      p sparky.public_disclosure          # => Sparky in human years is 28
      ```
    
    - *protected* method is in-between (public and private) approach
      - from *inside* the class, `protected` methods are accessible just like `public` methods
        - accessible
      - from *outside* the class, `protected` methods act just like `private` methods
        - not accessible
      - not used often
    
      ```ruby
      class Animal
        def a_public_method
          "Will this work? " + self.a_protected_method
        end

        protected

        def a_protected_method
          "Yes, I'm protected!"
        end
      end

      fido = Animal.new
      fido.a_public_method        # => Will this work? Yes, I'm protected!
      fido.a_protected_method
        # => NoMethodError: protected method `a_protected_method' called for
          #<Animal:0x007fb174157110>
      ```

### ACCIDENTAL METHOD OVERRIDING

  - Every class created inherently subclasses from class Object
  - Object class is built into Ruby and comes with methods
    - *Methods defined in the Object class are available in all classes*
      - i.e. available in Parent class
  - If a method is defined in a subclass and has the same name as a method in Object class
    - That method will be overwritten and all the objects of that subclass will use the custom method instead of the method from Object (superclass)

  ```ruby
  class Parent
    def say_hi
      p "Hi from Parent."
    end
  end

  Parent.superclass       # => Object

  class Child < Parent
    def say_hi
      p "Hi from Child."
    end

    def send
      p "send from Child..."
    end
  end

  child = Child.new
  child.say_hi         # => "Hi from Child."
  lad.send :say_hi     # => "Hi from Child." => without send method defined in Child class 
  lad.send :say_hi     # => ArgumentError: wrong number of arguments (1 for 0)
                         # => with send method defined in Child class 
  ```

  - say_hi method within Child class overwrites say_hi method within Parent class
  - `send` method is a predefined method in Object class
    - Overwritten by Child class
      - ArgumentError because the original send method takes in arguments
  - **Become familiar with the common Object methods to not accidentally override them**