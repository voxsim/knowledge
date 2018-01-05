# Ruby

## Identifiers
The first characters of a name indicate how the name is used.
- Local variables, method parameters, and method names should all start with a lowercase letter or with an underscore
- Global variables are prefixed with a dollar sign ($)
- Instance variables begin with an ``at'' sign (@)
- Class variables start with two ``at'' signs (@@)
- Class names, module names, and constants should start with an uppercase letter
- Symbols start with `:`

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

### Array
`Array`s are a lot like `Hash`es, except that the keys are always consecutive numbers, and always starts at 0.
In addition, all the methods that you just learned with `Hash`es can also be applied to `Array`s.

```ruby
array1 = ["hello", "this", "is", "an", "array!"]
```

### Strings

```ruby
"Danger, Will Robinson!"
```

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
TODO

### Nil
TODO

## Execution context

## Scoping

## Deconstructuring

## Looping

## Operators

## Error Handling

## Comments

In Ruby, any text on a single line that follows a # is a comment, and is ignored by the Ruby interpreter at run time.

    # comment

## Function Calls

Parentheses can sometimes be omitted. If you're not sure whether they're required, put them in. To be safe, put them in whenever the call is at all complicated. Even one as simple as this.

    puts "hello"
    puts("hello")
    assert_equal(5, number)

## Variables

Ordinary (local) variables are created through assignment:

    number = 5

Now the variable _number_ has the value _5_. Ordinary variables begin with lowercase letters. After the first character, they can contain any alphabetical or numeric character. Underscores are helpful for making them readable:

    this_is_my_variable = 5

A variable's value is gotten simply by using the name of the variable. The following has the value 10:

    number + this_is_my_variable # returns 10

## Strings, Objects and Methods

Strings are sequences of text in quotation marks. You can use single or double quotes.

    name = 'simon'
    name = "simon"

Strings are objects in Ruby. This means that they have methods. (In fact everything in Ruby is an object.)

A method call looks like this:

    "simon".upcase # returns "SIMON"

A method is a function for a particular type of object. In this case, the thing before the period is the object, in this case a string _simon_. The method is _upcase_. It capitalizes its object.

Like functions, methods can have arguments.

    "bookkeeper".include?('book') # returns true

This method is _true_ if its argument _book_ is a substring of _bookkeeper_.

You can also concatenate strings using the + operator.

    "dog" + "house" # returns "doghouse"

## Conditionals (if)

    if number == 5
      puts "Success" # "Success" is a string. Strings can be surrounded with single or double quotes.
    elsif number == 6
      puts "Acceptable"
    else
      puts "FAILURE"
    end

Put the _if_, _elsif, else_, and _end_ on separate lines as shown. You don't have to indent, but you should.

## Function Definitions

    def assert_equal(expected, actual)
      if expected != actual
        puts "FAILURE!"
      end
    end

Functions can return values, and those values can be assigned to variables. The return value is the last statement in the definition. Here's a simple example:

    def five # note that no parentheses are required
      5
    end
    box = five # box's value is 5

Note that we didn't need to say _five()_, as is required in some languages. You can put in the parentheses if you prefer.

The value of the last statement is always the value returned by the function. Some people like to include a _return_ statement to make this clear, but it doesn't change how the function works. This does the same thing:

    def five
      return 5
    end

Here's a little more complicated example:

    def make_positive(number)
      if number < 0
        -number
      else
        number
      end
    end
    variable = make_positive(-5) # variable's value is 5
    variable = make_positive(five) # variable's value is 5

## Libraries

Libraries contain functions or methods that can be used in many Ruby programs. Suppose we store the _make_positive_ function defined above in a file called _mathplus.rb_.

To use it in another script, we must _require_ it:

    require 'mathplus'

This will cause Ruby to search its _loadpath_ for a file named _mathplus.rb_. (It will automatically add the _.rb_.) It will search the directories that normally contain Ruby libraries, as well as the current directory (typically the same directory as your script).

If your library is in a location that Ruby doesn't know about, you will need to change the loadpath:

    $LOAD_PATH << 'c:/my_lib/'

Make sure you include this line _before_ you require libraries in it.

## Arrays

This is an array with nothing in it:

    []

This is an array with two numbers in it:

    [1, 2]

This is an array with two numbers and a string in it. You can put anything into an array.

    [1, 'hello!', 220]

Here's how you get something out of an array:

    array = [1, 'hello', 220]
    array[0] # value is 1

Here's how you get the last element out:

    array[2] # value is 220

Here's another way to get the last element:

    array.last # value is 220

Here's how you change an element:

    array[0]= 'boo!' # value printed is 'boo!'
    # array is now ['boo', 'hello', 220]

How long is an array?

    array.length # value is 3

Here's how you tack something onto the end of an array:

    array.push('fred') # array is now ['boo', 'hello', 220, 'fred']

## Iteration

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

## Regular Expressions

Regular expressions are a useful feature common to many languages. They allow you to match patterns in strings.

Regular expressions are characters surrounded by _//_ or _%r{}_. A regular expression is compared to a string like this:

    regexp =~ string

Most characters in a regular expression match the same character in a string. So, these all match:

    /a/ =~ 'a string'
    /a/ =~ 'string me along'

This also matches:

    /as/ =~ 'a string with astounding length'

Notice that the regular expression can match anywhere in the string. If you want it to match only the beginning of the string, start it with a caret:

    /^as/ =~ 'alas, no match'

If you want it to match at the end, end with a dollar sign:

    /no$/ =~ 'no match, alas'

If you want the regular expression to match any character in a string, use a period:

    /^.s/ =~ "As if I didn't know better!"

There are a number of other special characters that let you amazing and wonderful things with strings. Ruby uses the standard syntax for regular expressions used in many scripting languages. See _Programming Ruby_ for more information about regular expressions.

## Truth and Falsehood

If you try the examples above, you'll see that the ones that match print a number. That's the position of the first character in the match. The first expression (_/a/ =~ 'a string'_) returns _0_. (Ruby, like most programming languages, starts counting with 0.) The second returns _10_.

What happens if there's no match? Type this:

    /^as/ =~ 'alas, no match'

and the result will be _nil_, signifying no match. You can use these results in an _if_, like this:

    if /^as/ =~ some_string
      puts 'the string begins with "as".'
    end

In Ruby, anything but the two special values _false_ and _nil_ are considered true for purposes of an _if_ statement. So match results like _0_ and _10_ count as _true_.

## Blocks

A block is like a function without a name. It contains a set of parameters and one or more lines of code. Blocks are used a lot in Ruby. Iterators like _each_ use blocks.

Here's how to search an array for an element:

    gems = ['emerald', 'pearl', 'ruby']
    gems.detect { |gem| /^r/ =~ gem } # returns "ruby"

The _detect_ method takes a block as an argument. This block returns _true_ if the first argument starts with an _r_. (Actually it returns _0_, which counts as _true_.) The _detect_ method itself returns the first element for which its block is true.

When blocks are longer than one line, they are usually written using _do_ and _end_. This is another way of writing the same code:

    gems.detect do |gem|
      /^r/ =~ gem
    end

## Dictionaries

A _dictionary_ lets you say "Give me the _value_ corresponding to _key_." Dictionaries are also called _hashes_ or _associative arrays_.

Here's how you create a dictionary:

    dict = {}

Here's how you associate a value with a key:

    dict['bret'] = 'texas' # looks a lot like an array, except that the key doesn't have to be a number.

Here's how you retrieve a value, given a key:

    dict['bret'] # value is 'texas'.

Here's how you ask how many key/value pairs are in the dictionary:

    dict.length # value is 1

What values does a dictionary have?

    dict.values # value is the Array ['texas'].

What keys does it have?

    dict.keys # value is the Array ['bret'].

## Expression Substitution

Expression substitution evaluates an expression within a string:

You can do this

    name = "Aidy"
    puts "My name is: #{name}"

    => My name is: Aidy

And this:

    puts "The sum of four times four is: #{4*4}"

    => The sum of four times four is: 16
