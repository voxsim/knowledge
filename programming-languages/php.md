## String

### Interpolation

```php
// String with single quotes.
$panda = 'Pandas rule!';

// String with double quotes.
$panda = "Pandas rule!";
```

String with double quotes do interpolation. It's best to wrap interpolated values within { curly braces }. It makes the interpolation much cleaner, and you'll find it will work better when you start using arrays.

```php
// Set a string.
$value = 'pandas';

// Insert value.
$result = "We love {$value}!";

// Output.
var_dump($result);
```

### Concatenation

```php
// First value.
$first = 'Pandas are';

// Second value.
$second = ' awesome!';

// Concatenate.
var_dump($first . $second);
```

`.` try to cast both in string and concatenating them, `+` instead try to cast both in integer, if the data is to complex, then is equal to int(0).

## Array

### Indexed

```php
// Create an array.
$pandas = array('Lushui', 'Jasmina', 'Pali');

// Literal version
$pandas = ['Lushui', 'Jasmina', 'Pali'];
```

### Associative

```php
// Create an associative array.
$numbers = [
    'one'       => 1,
    'two'       => 2,
    'three'     => 3,
    'four'      => 4,
    'five'      => 5,
    'six'       => 6
];
```

### Multidimensional

```php
// Create a multi-dimensional array.
$numbers = [
    'prime'         => [2, 3, 5, 7, 11],
    'fibonacci'     => [1, 1, 2, 3, 5],
    'triangular'    => [1, 3, 6, 10, 15]
];
```

## Casting

just do (type) variable.

```php
// Set a string value.
$panda = '3';

// Cast to integer.
$panda = (int) $panda;

// Dump result.
var_dump($panda);
```

## Comments

```php
// mono line

/* */ multi line
```

## Forks

### If/Else/Elseif
```php
$panda = _SOMETHING_;

if ($panda == 'Lushui') {
    echo 'Yey, Lushui time!';
} elseif ($panda == 'Pali') {
    echo 'Oh hey there Pali!';
} elseif ($panda == 'Jasmina') {
    echo 'Looking pretty Jasmina!';
} else {
    echo 'Sorry, who are you?';
}
```

### Switch

```php
$panda = _SOMETHING_;

switch ($panda) {

    case 'Lushui':
        echo 'Yey, Lushui time!';
        break;

    case 'Pali':
        echo 'Oh hey there Pali!';
        break;

    case 'Jasmina':
        echo 'Looking pretty Jasmina!';
        break;

    default:
        echo 'Sorry, who are you?';
}
```


## Loops

### While
```php
// Set the panda counter to zero.
$pandas = 0;

// Iterate while $pandas less than 50.
while ($pandas < 50) {

    // Output the number of panda butlers.
    echo "We have {$pandas} panda butlers!\n";

    // Increment the counter.
    $pandas++;
}
```

### Do/While
```php
// Set the panda counter to zero.
$pandas = 0;

// Iterate...
do {

    // Output the number of panda butlers.
    echo "We have {$pandas} panda butlers!\n";

    // Increment the counter.
    $pandas++;

// ... while $pandas less than 50.
} while ($pandas < 50);
```

### For
```php
// Iterate for 50 repetitions.
for ($i = 0; $i < 50; $i++) {

    // Output the number of panda butlers.
    echo "We have {$i} panda butlers!\n";
}
```

### Foreach
```php
// Create an array of pandas.
$pandas = ['Lushui', 'Pali', 'Jasmina'];

// Iterate our panda array.
foreach ($pandas as $panda) {
    echo "Hello there {$panda}!\n";
}
```

### Control
`break` or `continue`.

## Function
```php
// Create a function.
function getMeaningOfLife() {

    // Return a value.
    return 42;
}

// Dump the result of the function.
var_dump(getMeaningOfLife());
```

### Varadic functions

```php
function welcome() {

    // Get all function parameters.
    $names = func_get_args();

    // Iterate the names and welcome them.
    foreach ($names as $name) {
        echo "Welcome, {$name}!\n";
    }
}

welcome('Dayle', 'James', 'Andrea', 'Ben', 'Mateusz');
```

### Type Hinting
Type declarations allow functions to require that parameters are of a certain type at call time. If the given value is of the incorrect type, then an error is generated: in PHP 5, this will be a recoverable fatal error, while PHP 7 will throw a TypeError exception.

```php
// Say hello to an array of people.
function sayHello(array $names) {
    foreach ($names as $name) {
        echo "Hello, {$name}!\n";
    }
}

sayHello(['Katie', 'Corissa', 'Lucy']);
```

Before PHP7 you can't type hinting with scalar types (string, int, etc..).

### Closures

```php
$cat = function () {
    echo 'Oh long Johnson!';
};
```

### Closures with functions as arguments

```php
// Create a math function.
function math(Closure $type, $first, $second) {

    // Execute the closure with parameters
    return $type($first, $second);
}

// Create an addition closure.
$addition = function ($first, $second) {

    // Add the values.
    return $first + $second;
};

// Create an subtraction closure.
$subtraction = function ($first, $second) {

    // Subtract the values.
    return $first - $second;
};
```

### Return Type Declarations

```php
function pandaSeven() : int {
    return 3;
}
```

## Include / Require
If you try to `include` a file that doesn't exist, then PHP will show a warning message, and continue executing. If this is a problem in our applications, we can use the `require` statement instead of the include to have PHP throw a fatal error when the file cannot be loaded.

With `require_once` any other require will be ignored.

## Classes

```php
// Define the Panda class.
class Panda
{
    // LOUD NAME PROPERTY
    private var $loudName;

    // Contructor method.
    function __construct($name)
    {
        $this->loudName = $this->makeNameLoud($name);
    }

    // NAME LOUDENING METHOD
    public function makeNameLoud($name)
    {
        return strtoupper($name);
    }
}

$panda = new Panda('Lushui');

class GiantPanda extends Panda
{
    var $coat = 'less fluffy';
}
```

### Scopes
- private
- public
- protected

## Constants

### Global
```php
// Define our constant.
define('PI', 3.14159265359);

// Echo the value of PI.
echo PI;

// From PHP7 you can define array as constants
define('PANDA', ['Awesome!', 'Great!', 'Fluffy!']);
```

### Class
```php
class Circle
{
    /**
     * The value of PI.
     */
    const PI = 3.14159265359;

    /**
     * Calculate the circumference of a circle from diameter.
     *
     * @param  mixed $diameter
     * @return mixed
     */
    public function circumference($diameter)
    {
        return $diameter * self::PI;
    }
}
```
The value of PI is now immutable, and PHP will throw an error if you attempt to change it. The const value is static and bounded to the class.

### Anonymous
```php
$panda->eat(new class {
    public function noise()
    {
        return 'Crunch!';
    }
});
```

## Abstract class

```php
abstract class Animal
{
    /**
     * Is the animal awesome (all are).
     *
     * @var boolean
     */
    private $awesome = true;

    /**
     * Access the awesome attribute.
     *
     * @return boolean
     */
    public function isAwesome()
    {
        return $this->awesome;
    }
    
     abstract public function makeNoise();
}
```

Abstract classes can't be instantiated and abstract function have to be implemented by the classes that inherits Animal.

## Interfaces

```php
interface PandaInterface
{
    /**
     * Eat some food!
     */
    public function eat($food);

    /**
     * Poop! (Normally after eating.)
     */
    public function poop();

    /**
     * Sleepy time!
     */
    public function sleep($time);
}
```

```php
class RedPanda implements PandaInterface
{

}
```

With interfaces we can achieve polymorphism.

## Statics

```php
class RedPanda
{
    /**
     * The panda's name!
     *
     * @var string
     */
    public static $name;
}

RedPanda::$name = 'Hamish';

echo RedPanda::$name;
```

### Late Static Binding
the self keyword will only reference the base class. If we wish to use late static binding, we need to replace the `self` keyword with `static`. Yes, I know... we sure are overusing this keyword. Let's take a look at the transformation.

```php
class Panda
{
    public static function whoAmI()
    {
        return static::getType();
    }

    public static function getType()
    {
        return 'I am a Giant panda!';
    }
}

class RedPanda extends Panda
{
    public static function getType()
    {
        return 'I am a Red panda!';
    }
}

echo Panda::whoAmI(); // I am a Giant panda!
echo RedPanda::whoAmI(); // I am a Red panda!
```

## Exceptions

### Throw
```php
throw new Exception('NO CHOCOLATE FOR THE PANDA!');
```

### Try/catch
```php
// Set the type of food.
$food = 'chocolate';

try {
    feedPanda($food);
} catch (PandaChocolateException $exception) {
    echo 'That was a close one! No chocolate for the panda.';
} finally {
    // Code to run after the try and catch.
}
```

## Trait
Trait is a way to achieve multiple inheritance.

```php
rait TestTrait
{
    public function test()
    {
        echo 'This is the trait method.';
    }
}

class TestClass
{
    public function test()
    {
        echo 'This is the class method.';
    }
}

// Define a class which extends the baseclass
// and implements the trait.
class Testing extends TestClass
{
    use TestTrait;
}

// Create our testcase.
$test = new Testing;

// Run the test method.
$test->test(); // It will print 'This is the trait method.' because the trait method wins.
```

## Namespacing

```php
namespace Baratheon;

use Dayle\Blog as Cms;

// app/routes.php

$post = new Cms\Content\Post;
$page = new Cms\Content\Page;
$tag  = new Cms\Tag;
```

### Group Use Declarations

```php
namespace OtherNamespace;

use Animal\Panda\{Red as Lushui, Giant, Fluffy};
```

## Null Coalesce Operator

Before PHP7
```php
if (isset($panda)) {
    echo $panda;
} else {
    echo 'Giant Panda';
}

// or...

echo isset($panda) ? $panda : 'Giant Panda';
```

after

```php
echo $panda ?? 'Giant Panda';
```

## Spaceship operator

```
$tom = 3 <=> 4;

// <=> is equal to

$a > $b : +1
$a = $b :  0
$a < $b : -1
```

## Command Line Interface
The -i option will print your PHP configuration just like the phpinfo() function.

The -a option provides an interactive shell, similar to ruby’s IRB or python’s interactive shell. There are a number of other useful command line options, too.

Let’s write a simple “Hello, $name” CLI program. To try it out, create a file named hello.php, as below.

```php
<?php
if ($argc !== 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
```

PHP sets up two special variables based on the arguments your script is run with. $argc is an integer variable containing the argument count and $argv is an array variable containing each argument’s value. The first argument is always the name of your PHP script file, in this case hello.php.

The exit() expression is used with a non-zero number to let the shell know that the command failed.

- http://www.phptherightway.com/#coding_practices
- http://www.php-fig.org/psr/psr-0/
- http://www.php-fig.org/psr/psr-1/
- http://www.php-fig.org/psr/psr-2/
- http://www.php-fig.org/psr/psr-4/
- http://php.net/language.oop5
- http://php.net/language.oop5.traits
- http://php.net/functions.anonymous
- http://php.net/class.closure
- https://wiki.php.net/rfc/closures
- http://php.net/language.types.callable
- http://php.net/function.call-user-func-array
- http://php.net/language.oop5.magic
- http://php.net/intro.reflection
- http://php.net/language.oop5.overloading
- http://php.net/language.namespaces
- http://php.net/book.spl
- http://php.net/features.commandline.options
- http://www.gsp.com/cgi-bin/man.cgi?section=3&topic=sysexits
- http://symfony.com/doc/current/contributing/code/standards.html
- https://github.com/phptodayorg/php-must-watch
- http://php.net/manual/en/langref.php
- http://www.php-fig.org/psr/psr-3/
- http://www.php-fig.org/psr/psr-6/
- http://www.php-fig.org/psr/psr-7/
- http://www.php-fig.org/psr/psr-11/
- http://www.php-fig.org/psr/psr-13/
- http://www.php-fig.org/psr/psr-16/
