# METHODS

`puts` to print with new line

`print` to print without new line

`#` comments

`#{}` to include Ruby code inside string

`gets` method to read user input
  - program waits for user input
  - get back a *string* with a *new line character \n*

`gets.chomp` removes the new line character \n from gets
  - if .chomp is not included, if condition would not be met

  ```ruby
  name = gets

  if name == "David"
    puts "Hello David, we were expecting you!"
  end
  ```

`$stdin.gets.chomp` allows user input when AGRV (argument variable) is used

  ```ruby
  first, second, third = ARGV

  puts "Your first variable is: #{first}"
  puts "Your second variable is: #{second}"
  puts "Your third variable is: #{third}"

  print "Give me a number:"
  number = $stdin.gets.chomp # using gets.chomp will throw error
  puts "Number is #{number}"
  ```

`.to_i` converts to number
`.to_f` converts to float

  ```ruby
  number = gets.chomp.to_i # 22 => 22
  
  another_number = gets.chomp # 22
  another_number.to_i # 22

  new_number = gets.chomp.to_f # 22 => 22.0
  ```
  
`.strip` removes white spaces from the beginning and end
`.chop` removes the last character
  
  ```ruby
  a = '  f f   f     f     '
  a.strip # 'f f   f     f'

  b = 'abcde'
  b.chop # 'abcd'
  ```

`.. and ...`
  - `..` from the beginning to the end
  - `...` exclude the end value

 ```ruby
  (1..5).to_a # [1, 2, 3, 4, 5] 

  (1...5).to_a # [1, 2, 3, 4] 
```

`=~` operator for matching regular expressions
  - returns the index of the start of the match
  - nil if no match

```ruby
s = 'how now brown cow'

s =~ /cow/ # => 14
s =~ /now/ # => 4
s =~ /cat/ # => nil
```

<hr>

# OBJECT CLASS METHODS

`time` abstraction of dates and times
  - create an instance of Time with `::now` or `.now`
    - takes arguments such as year, month, minute, etc.

```ruby
Time.now(2002)         # => 2002-01-01 00:00:00 -0500
Time.now(2002, 10)     # => 2002-10-01 00:00:00 -0500
Time.now(2002, 10, 31) # => 2002-10-31 00:00:00 -0500

t = Time.now(1993, 02, 24, 12, 0, 0, "+09:00")
t.monday?              # => false
t.year                 # => 1993
```

<hr>

# ARRAY METHODS

  - If `!` is placed after the method, the *new array will be saved* to the array that was called

`.find(if_none_proc = nil) { ...block }` returns the first element for which the block returns a truthy value
  - if no such element found, calls if_none_proc and returns its return value
  - if no block given, returns an Enumerator

  ```ruby
  (0..9).find {|element| element > 2}                # => 3
  (0..9).find(proc {false}) {|element| element > 12} # => false
  {foo: 0, bar: 1, baz: 2}.find {|key, value| key.start_with?('b') }            # => [:bar, 1]
  {foo: 0, bar: 1, baz: 2}.find(proc {[]}) {|key, value| key.start_with?('c') } # => []
  ```

`.select { ...block }` returns an array containing elements selected by the block
  - returns an array with elements which the block returns a truthy value
  - with no block given, returns an Enumerator

  ```ruby
  (0..9).select {|element| element % 3 == 0 } # => [0, 3, 6, 9]
  a = {foo: 0, bar: 1, baz: 2}.select {|key, value| key.start_with?('b') }
  a # => {:bar=>1, :baz=>2}
  ```

`.shift(n)` removes the first element of the array and returns the element
  - if (n) is given, the first n elements
  ```ruby
  args = [ "-m", "-q", "filename" ]
  args.shift     #=> "-m"
  args           #=> ["-q", "filename"]

  args = [ "-m", "-q", "filename" ]
  args.shift(2)  #=> ["-m", "-q"]
  args           #=> ["filename"]
  ```


`.shuffle` returns a new array with elements of self shuffled
  ```ruby
  a = [ 1, 2, 3 ]           #=> [1, 2, 3]
  a.shuffle                 #=> [2, 3, 1]
  a                         #=> [1, 2, 3]
  a.shuffle!                #=> [2, 3, 1]
  a                         #=> [2, 3, 1]
  ```

`.sort` randomly sorts an array and returns the sorted array
  - if a block is given, comparisons in the block determine the ordering
    - <=> operator - *|a, b| b <=> a*
      - A negative integer if a < b.
      - Zero if a == b.
      - A positive integer if a > b.
  ```ruby
  ary = [ "d", "a", "e", "c", "b" ]
  ary.sort                     #=> ["a", "b", "c", "d", "e"]
  ary                          #=> ["d", "a", "e", "c", "b"]
  ary.sort!                    #=> ["a", "b", "c", "d", "e"]
  ary                          #=> ["a", "b", "c", "d", "e"]

  a = %w[b c a d]
  a.sort {|a, b| b <=> a } # => ["d", "c", "b", "a"]
  h = {foo: 0, bar: 1, baz: 2}
  h.sort {|a, b| b <=> a } # => [[:foo, 0], [:baz, 2], [:bar, 1]]
  ```

`.sort_by` with a block given, returns an array of elements sorted according to the value returned by the block for each element
  - multiple parameters can be included
  ```ruby
  a = %w[xx xxx x xxxx]
  a.sort_by {|s| s.size }               # => ["x", "xx", "xxx", "xxxx"]
  a.sort_by {|s| -s.size }              # => ["xxxx", "xxx", "xx", "x"]
  a.sort_by {|s| s.size }.reverse       # => ["xxxx", "xxx", "xx", "x"]

  # sort by multiple parameters
  candidates.sort_by! { |candidate| [candidate[:years_of_experience], candidate[:github_points]] }.reverse
  ```

<hr>