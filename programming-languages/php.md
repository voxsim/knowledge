# PHP

I need to read:
- http://php.net/manual/en/migration56.new-features.php
- http://php.net/manual/en/migration70.new-features.php

## Features from PHP 7.1 (http://php.net/manual/en/migration71.new-features.php)

### Nullable types

Type declarations for parameters and return values can now be marked as nullable by prefixing the type name with a question mark. This signifies that as well as the specified type, null can be passed as an argument, or returned as a value, respectively.

```php
function testReturn(): ?string
{
  return 'elePHPant';
}

var_dump(testReturn());

function testReturn(): ?string
{
  return null;
}

var_dump(testReturn());

function test(?string $name)
{
  var_dump($name);
}

test('elePHPant');
test(null);
test();
```

The above example will output:

```
string(10) "elePHPant"
NULL
string(10) "elePHPant"
NULL
Uncaught Error: Too few arguments to function test(), 0 passed in...
```

### Void functions

A void return type has been introduced. Functions declared with void as their return type must either omit their return statement altogether, or use an empty return statement. null is not a valid return value for a void function.

### Symmetric array destructuring

The shorthand array syntax ([]) may now be used to destructure arrays for assignments (including within foreach), as an alternative to the existing list() syntax, which is still supported.

```php
$data = [
  [1, 'Tom'],
  [2, 'Fred'],
];

// list() style
list($id1, $name1) = $data[0];

// [] style
[$id1, $name1] = $data[0];

// list() style
foreach ($data as list($id, $name)) {
  // logic here with $id and $name
}

// [] style
foreach ($data as [$id, $name]) {
  // logic here with $id and $name
}
```

### Class constant visibility
```php
class ConstDemo
{
    const PUBLIC_CONST_A = 1;
    public const PUBLIC_CONST_B = 2;
    protected const PROTECTED_CONST = 3;
    private const PRIVATE_CONST = 4;
}
```

### iterable pseudo-type ¶
A new pseudo-type (similar to callable) called iterable has been introduced. It may be used in parameter and return types, where it accepts either arrays or objects that implement the Traversable interface. With respect to subtyping, parameter types of child classes may broaden a parent's declaration of array or Traversable to iterable. With return types, child classes may narrow a parent's return type of iterable to array or an object that implements Traversable.

```php
function iterator(iterable $iter)
{
    foreach ($iter as $val) {
        //
    }
}
```

### Multi catch exception handling
Multiple exceptions per catch block may now be specified using the pipe character (|). This is useful for when different exceptions from different class hierarchies are handled the same.

```php
try {
    // some code
} catch (FirstException | SecondException $e) {
    // handle first and second exceptions
}
```

### Support for negative string offsets for string manipulation functions and string indexing

### Convert callables to Closures with Closure::fromCallable()
A new static method has been introduced to the Closure class to allow for callables to be easily converted into Closure objects.

```php
class Test
{
    public function exposeFunction()
    {
        return Closure::fromCallable([$this, 'privateFunction']);
    }

    private function privateFunction($param)
    {
        var_dump($param);
    }
}

$privFunc = (new Test)->exposeFunction();
$privFunc('some value');
```
