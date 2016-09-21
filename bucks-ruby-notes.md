# Buck's Ruby Notes

## Environment
### Interpreters
- irb is the standard console interpreter  
- pry is an alternative that does nice formatting and color-coding of Ruby objects

## Outputting for testing, debugging, diagnostics
- print is simplest: outputs string to console, returns nil  
- puts is next simplest: outputs string to console with a newline, returns nil  
- p gives the most info for debugging: it outputs results of call to inspect, and returns the evaluated code

## Getting Input from Console
```ruby
puts 'Hello there, what\'s your name?'
name = gets.chomp
puts 'Hello, ' + name + '!'
```

## Basic Syntax

### Nil not Null
It's nil in Ruby, not null.

### Comments

```ruby
# This is a comment
# Most people do multiline comments like
# this.

=begin
Multiline comments can be put between =begin and =end, but not many people do this
=end
```

### Semicolons
    Not needed (and it's typically considered good style not to use them),
    unless two statements are on the same line, then they need to be separated by a semicolon

### Quotes
Single quotes and double quotes are the same except:
- Double quotes must be used if you're doing string interpolation: "Hello #{world_name}"
- Double quotes must be used when escaping characters: 'a\nb' evaluates to string a\nb; "a\nb" evaluates to a, newline, b
  - Except that you can use single quotes to escape single quotes: 'you\'re'

### Variables

#### Assignment
```ruby
composer = 'Mozart'
composer_age = cur_year - composer_yob
```

### Flow Control

```ruby
if name == 'Buck'
  puts 'Hello Mr. Melton'
end

if name == 'Buck'
  puts 'Hello Mr. Melton'
else
  puts 'Who are you, stranger?'
end

if name == 'Buck'
  puts "Howdy pardner."
elsif name == 'Katie'
  puts 'What a lovely name!'
end

loop do
    # something
    break if <test is true>
end

while input != 'bye'    # no 'do' needed
  puts 'Enter:'
  input = gets.chomp
end

until coder.top_ranked?     # no 'do' needed.  equivalent to 'while not'
    coder.practice
end

# Same as above
coder.practice until coder.top_ranked?

break
next    # like 'continue' in other languages
```
### Data Structures

#### Array
##### Create New Array
```ruby
langs = ['English', 'Hawaiian', 'Portuguese']
array_2 = [] # create empty array
array_2 = Array.new # same, creates empty array
```

##### Methods on Array
```ruby
keep_if # return array of just the elements passing test
[0..7].keep_if {|x| x.even?}    #=> [0,2,4,6]

length
reverse
each
langs.each do |lang|
  puts 'I love ' + lang
end

# Alternatively:
langs.each {|lang| puts 'I love ' + lang}

join
puts langs.join(' - ') # Yields 'English - Hawaiian - Portuguese'

push    # pushes element onto end of array
pop     # pops the last elemnet of the array

last    # returns the last element of the array, but leaves the array untouched
```

#### Hash
##### Create new hash
```ruby
my_hash = {}  # creates empty hash
my_hash = Hash.new  # same, creates empty hash
my_hash = Hash.new('month') # same, with default value of 'month' if the key or value doesn't exist

# Keys are strings
currencies_hash = { 'United States' => 'dollar',
                    'Canada' => 'dollar',
                    'Great Britain => 'pound'
                  }

currencies_hash['United States']  # evaluates to 'dollar'

# Keys are symbols
my_info = { first_name: 'Buck',
            last_name: 'Melton',
          }

my_info[:first_name]  # evalutes to 'Buck'
```

##### Methods on Hash
```ruby
#each
currencies_hash.each do |country, currency|
  puts "The currency of #{country} is the #{currency}"
end
```

### Methods

#### Defining a Mathod
```ruby
def method_name (arg1, arg2, arg3) # parens optional
  # method body here
end
```

#### Calling a Method

object.method_name(arg1val, arg2val, arg3 val)

      Note many things we think of as 'operators' are methods
        Arithmetic operators:
          5 + 5 is just a shortcut for 5.+ 5 where "+" is a method on Integer
          6 * 4 is just a shortcut for 6.* 4 where "*" is a method on Integer
        Array operator:
          arr[2] is just a shortcut for arr.[] 2

#### Return values
Methods return the last expression evaluated in the method (which can be an explicity 'return', but doesn't have to be).

## Iterators
      #each
      #times
        3.times do
          puts 'Hip Hip Hooray! '
        end

        Alternatively:
          3.times { puts 'Hip Hip Hooray! '}


## Data Conversion

  Integer to Float: two ways: Float(3); 3.to_f
    I don't know why the 3.to_f works.  to_f is not a method on Integer or any of its ancestors, nor on the module Kernel.

## Files and Directories

  Write to a file:
```ruby
filename = 'buck.txt'
test_string = 'This is a test file.'

File.open filename, 'w' do |f|
  f.write test_string
end
```

  Read from a file:
`read_string = File.read filename`

  Find all files in a directory:
`my_files = Dir['*.jpg'] # returns an array of the matching filenames`

  Dir.chdir(new_path) # change directory
  File.rename(new_path_or_name) # rename/move file

## Objects

### Creating a new object
    Usually use the 'new' method:
```ruby
    alpha = Array.new # creates empty array
    beta = String.new # creates empty string
    now = Time.new # current date and time
```
    We can also create a new Array using an array literal: new_array = ['Buck', 'Ron', 'Gifford']
    We can also create a new String using a string literal: new_string = 'Buck'

## Classes/Modules

  Find the class of an object using the 'class' method
    some_random_object = 'Buck'
    some_random_object.class # returns 'String'

### Defining a class
```ruby
class Die

  def initialize
    roll
  end

  def roll
    @number_showing = 1 + rand(6)
  end

  def showing
    @number_showing
  end

end
```

Change an existing class  
Just define the class and add/change whatever you want, even including redefining existing methods (but not recommended: make a new method instead).

```ruby
    class Integer
      def to_english
        if self == 5
          english = 'five'
        elsif self == 42
          english = 'forty-two'
        end
      end
    end
```
#### Enumerable

Included in Array, Hash

##### Easy Methods
```ruby
first   # return the first element of the Enumerable
last    # return the last element of the Enumerable
max     # return max of Enumerable
sort    # sort the Enumerable
sort!   # sort the Enumerable in-place
```

##### Methods That Take Blocks
```ruby
inject  # Combine elements using some binary operation
[5..10].inject(0) {|product, num| product * num} #=> Multiply them all: 151200

detect  # return the first one that satisfies the block
[1,3,4,7,8].detect {|x| x.even?|}   #=> 4
[1,3,4,7,8].detect(&:even?) #=> 4. Exactly the same as above, with shortcut notation

reject  # remove all elements that pass the test
[1, 10, 20, 15, 25].reject {|x| x < 16 }    #=> [20, 25]
```


#### String

Converting a String to an Array
`the_ary = the_str.split("")``

Methods
```ruby
      length
      reverse

      upcase
      downcase
      swapcase
      capitalize

      center(line_width)
      ljust(line_width)
      rjust(line_width)

      # Substrings
      # The 8 characters starting with the 12th character
      my_string[12, 8]

      # The 12th through the 19th character (same as above, but using a range)
      my_string[12..19]

      # Count from end of string using negative numbers
      # last 4 characters:
      last_4 = my_string[-4..-1]
```
#### Number
    `abs`

#### Random
```ruby
    rand # just calling rand returns float >= 0 and < 1.
    rand(int) # returns integer >= 0 and < int.
```
#### Math
```ruby
    Math::PI
    Math::E
    Math.cos
    Math.tan
    Math.log
    Math.sqrt
```

#### Range
```ruby
    # This is a range literal.
    letters = 'a'..'e'

    # Convert range to array.
    `letter_ary = letters.to_a`

    # Iterate over range
('A'..'Z').each do |letter|
  print letter
end

#min
#max
#include?
letters.include?('b') # true
```
