# RSPEC

  - RSpec is one of the Ruby testing libraries
    - *Tests behaviour* rather than only specific methods

  - Tests written with RSpec are called *specs* (i.e. specifications)
    - Stored in spec directory

## THE BASICSS

  - RSpec give a way to encapsulate what is being tested via `describe` block
    - To describe the baheviour of a class
    - Tells RSpec *what code you are writing tests for*
  
  - Tests are written using the `it` block *between do and end*
    - `it` is a test
    - takes a string as a parameter - description of the feature being tested
  
  - `expect` method marks an *assertion* you are trying to make about the code you are testing
    - Pass an argument to expect method - return value
  
  - `to` method to complete the assertion, on the object returned from the call to the expect method

  - `be_a` matcher
    - Matchers are special methods that can check whether the argument passed to expect meets some criteria

  ```ruby
  require_relative 'boat'

  describe Boat do
    it 'should create boats' do
      expect(Boat.new).to be_a Boat # boat.is_a?
    end
  end
  ```

## TDD

  - `describe` block can be nested
  - `#` indicates an *instance method* of Boat

  ```ruby
  require_relative 'boat'

  describe Boat do
    it 'should create boats' do
      expect(Boat.new).to be_a Boat
    end

    describe '#allowed_aboard?' do
      it 'returns true if inventory includes a life jacket' do
        a_boat = Boat.new
        allowed = a_boat.allowed_aboard?(['life jacket', 'sun glasses'])
        expect(allowed).to be true
    end
  end
  ```
  