# Ruby

Eloquent ruby - chapter 5 - page 53

## Standard
* Camel case for classes, snake case for everything else.
* Everything is a class like this:

```ruby
class Document
  attr_accessor :title, :author, :content
  def initialize(title, author, content)
    @title = title
    @author = author
    @content = content
  end
  
  def words
    @content.split
  end
  
  def word_count
    words.size
  end
end
```
* Parentheses are optional
* Folding up lines like `puts doc.title; puts doc.author`
* Folding up code blocks like `10.times { |n| puts "The number is #{n}" }`
* The bang (!) in the end of a parameter usually means that you are doing an operation in place (e.g. a.reverse! it reverse a itself)
* Ruby arrays and hashes are ordered by default

## Identifiers
The first characters of a name indicate how the name is used.
- Local variables, method parameters, and method names should all start with a lowercase letter or with an underscore
- Global variables are prefixed with a dollar sign ($)
- Instance variables begin with an ``at'' sign (@)
- Class variables start with two ``at'' signs (@@)
- Class names, module names, and constants should start with an uppercase letter
- Symbols start with `:`

## Blocks

A block is like a function without a name. It contains a set of parameters and one or more lines of code. Blocks are used a lot in Ruby. Iterators like _each_ use blocks.

Here's how to search an array for an element:

```ruby
gems = ['emerald', 'pearl', 'ruby']
gems.detect { |gem| /^r/ =~ gem } # returns "ruby"
```

The _detect_ method takes a block as an argument. This block returns _true_ if the first argument starts with an _r_. (Actually it returns _0_, which counts as _true_.) The _detect_ method itself returns the first element for which its block is true.

When blocks are longer than one line, they are usually written using _do_ and _end_. This is another way of writing the same code:

```ruby
gems.detect do |gem|
  /^r/ =~ gem
end
```

## Function Definitions
```ruby
def assert_equal(expected, actual)
  if expected != actual
    puts "FAILURE!"
  end
end
```

Functions can return values, and those values can be assigned to variables. The return value is the last statement in the definition. Here's a simple example:

```ruby
def five # note that no parentheses are required
  5
end
box = five # box's value is 5
```

Note that we didn't need to say _five()_, as is required in some languages. You can put in the parentheses if you prefer.

The value of the last statement is always the value returned by the function. Some people like to include a _return_ statement to make this clear, but it doesn't change how the function works. This does the same thing:

```ruby
def five
  return 5
end
```

Here's a little more complicated example:

```ruby
def make_positive(number)
  if number < 0
    -number
  else
    number
  end
end
variable = make_positive(-5) # variable's value is 5
variable = make_positive(five) # variable's value is 5
```

To have any number of arguments you can do that:

```ruby
def add_authors( *names )
    @author += " #{names.join(' ')}"
end
```

## Classes
TODO

## Data types
There are eight primitive types and 3 more data types derived from the Numeric superclass.
Everything has a class.

### Constants
Two things to remember about constants:  
1\. Constants start with capital letters. `Constant` is a constant. `constant` is not a constant.  
2\. You can change the values of constants, but Ruby will give you a warning.

### Symbols
`Symbol`s are lightweight objects best used for comparisons and internal logic
Symbols are denoted by the colon sitting out in front of them, like so: `:symbol_name`

### Hashes
Hashes are like dictionaries. You have a key, a reference, and you look it up to find the associated object, the definition.

```ruby
hash = { :leia => "Princess from Alderaan", :han => "Rebel without a cause"}
```

and you can write this as:

```ruby
hash = { leia: "Princess from Alderaan", han: "Rebel without a cause"}
```

### Array
`Array`s are a lot like `Hash`es, except that the keys are always consecutive numbers, and always starts at 0.
In addition, all the methods that you just learned with `Hash`es can also be applied to `Array`s.

```ruby
array1 = ["hello", "this", "is", "an", "array!"]
```

and you can write this as:

```ruby
array1 = %w{hello this is an array!}
```

### Strings

```ruby
str = "Danger, Will Robinson!"
```

Ruby strings are mutable. If you assign the string to another string and change one of them, it will change the other.

Arbitrarily quoted strings always start with a percent sign (%) followed by the letter q. The character after the q is the actual string delimiter, usually we use `{`. The same example of before:

```ruby
str = %q{Danger, Will Robinson!}
```

#### Expression Substitution

Expression substitution evaluates an expression within a string:

You can do this

```ruby
    name = "Aidy"
    puts "My name is: #{name}"
```

=> My name is: Aidy

And this:

```ruby
puts "The sum of four times four is: #{4*4}"
```
=> The sum of four times four is: 16

### Numbers (Integers and Floats)

```ruby
string1 = 451.to_s
string2 = 98.6.to_s
int = 4.5.to_i
float = 5.to_f
``` 

`to_s` converts floats and integers to strings. `to_i` converts floats to integers. `to_f` converts integers to floats. There you have it. All the data types of Ruby in a nutshell. Now here's that quick reference table for string methods I promised you.

### Ranges
TODO

### Regular expressions
In Ruby, the regular expression, or Regexp for short,5 is one of the built-in data types, with its own special literal syntax. To make a Ruby regular expression you encase your pattern between forward slashes. For example:

```ruby
/\d\d:\d\d (AM|PM)/
```

### Nil
TODO

## Control Structures

### If, Unless, While, and Until

```ruby
if number == 5
  puts "Success" # "Success" is a string. Strings can be surrounded with single or double quotes.
elsif number == 6
  puts "Acceptable"
else
  puts "FAILURE"
end
```

```ruby
if not @read_only
  @title = new_title
end
```

```ruby
unless @read_only
  @title = new_title
end
```

```ruby
while ! document.is_printed?
  document.print_next_page
end
```

```ruby
until document.is_printed?
  document.print_next_page
end
```

And we can inline them.
Remember to use `@first_name ||= ''` instead of `@first_name = '' unless @first_name`

### Iteration

When you do something multiple times, it is called _iteration_. There are many ways to do this. The following will print _hello_ five times:

    5.times do
      puts 'hello'
    end

Here's one way to print the numbers from one to 10:

    for x in 1..10 do
      puts x
    end

And here's another:

    (1..10).each do |x|
      puts x
    end

The part between the _do_ and the _end_ is called a _block_. You can replace the _do_ and _end_ with braces:

    (1..10).each { |x| puts x }

The _1..10_ is a range, which works like an array of the numbers from 1 to 10. The _each_ is a method that iterates through each element of the range. It is called an _iterator_.

This prints each value of an array:

    ["a", "b", "c"].each { |x| puts x }

What if you want to transform each element of an array? The following capitalizes each element of an array.

    ["hi", "there"].collect { |word| word.capitalize } # The result is ["Hi", "There"].

### Switch

```ruby
author = case title
         when 'War And Peace' then 'Tolstoy'
         when 'Romeo And Juliet' then  'Shakespeare'
         else "Don't know"
         end
```

## Comments

In Ruby, any text on a single line that follows a # is a comment, and is ignored by the Ruby interpreter at run time.

```ruby
# comment
```

## Libraries

Libraries contain functions or methods that can be used in many Ruby programs. Suppose we store the _make_positive_ function defined above in a file called _mathplus.rb_.

To use it in another script, we must _require_ it:

    require 'mathplus'

This will cause Ruby to search its _loadpath_ for a file named _mathplus.rb_. (It will automatically add the _.rb_.) It will search the directories that normally contain Ruby libraries, as well as the current directory (typically the same directory as your script).

If your library is in a location that Ruby doesn't know about, you will need to change the loadpath:

    $LOAD_PATH << 'c:/my_lib/'

Make sure you include this line _before_ you require libraries in it.
