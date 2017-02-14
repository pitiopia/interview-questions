# PHP Interview Questions

Below you can find a list of most common questions that might occur during Java Interview.

This file is a part of bigger set of [IT Interview Questions](../../README.md)

# Questions

#### :bangbang: Name 5 important changes of PHP 7 comparing to 5.6  :bangbang:

There are much more changes in PHP 7 than only five. As always there are some removals of old deprecated code, as well as 
introduction to new useful functions. It is recommended to remember at least 5 of them:

1. Some deprecated features have been removed:
    * all alternative tags like `<script language="php">...</script>` and ASP syntax `<% ... %>` and `<%=$var; %>`
    * all POSIX-compatible methods like `ereg()`, `eregi()`, `split()`, `ereg_replace()` and other - now you should use `preg_` family of functions
    * multiple `default` clauses in `switch` statements were disables - now `Fatal Error: Switch statements may only contain one default clause` will be thrown
    * whole `mysql` extension - it is recommended to migrate to mysqli or PDO extension
2. Uniform Variable Syntax has been implemented - which fixed inconsistency of using variable-variable and variable-property structure (you have to be aware that the new syntax isn't fully backward-compatible)
3. Null coalesce operator `??` has been introduced -  `$foo = $bar ?? $baz;` which is equal to `$foo = isset($bar) ? $bar : $baz;`
4. Combined comparision operator `<=>` (called spaceship operator) was introduced - first trinary operator in PHP - `$a <=> $b` is an equivalent of `($a < $b) ? -1 : (($a > $b) ? 1 : 0)` 
5. Usage of `define()` method has been unified to the constants defined by `const` - now both can assign them array values
6. `list()` now supports objects that implement `\ArrayAccess` interface
7. `intdiv()` function has been introduced to perform integer divisions, which is a inverse of modulo operator
8. `preg_replace_callback_array()` has been introduced to perform multiple regular expressions replacements with different callbacks for each of the expressions
9. `random_bytes()` and `random_int()` functions introduced to improve randomness of generated integers and strings
10. `options` parameter has been added to `session_start()` function. `lazy_write` option which set to `true` (default) says that session data is rewritten only when there were any changes in it
11. `options` parameter has been added to `unserialize()` that accepts `allowed_classes` option that defines which class names should be instantiated. All other will be returned as instance of `__PHP_Incomplete_Class`
12. `dirname()` function accepts `levels` parameter which defines how many levels it should go up in the dir hierarchy
13. `password_hash()` function  is now deprecated
14.  You can now enable zero-cost assertions through INI configuration ( set `zend.assertions` to -1 ), as well as throw exceptions instead of warnings ( just set `assert.exceptions` to 1 )
15. According to [__Exceptions in the engine RFC__](https://wiki.php.net/rfc/engine_exceptions_for_php7) all fatal errors and catchable fatal errors have been changed to throw \Error which is a sibling of \Exception (there are also other changes that cna be found on the RFC page)
16. Unicode Codepoint Escape Syntax was introduced [read more on RFC page](https://wiki.php.net/rfc/unicode_escape)
17. The `IntlChar` class has been introduced [read more on RFC page](https://wiki.php.net/rfc/intl.char)
18. `Closure` class introduces new `call()` method which sets new scope for the given closure
19. Generators improvements have been introduced ( [more info on RFC page](https://wiki.php.net/rfc/generator-return-expressions) )
20. Changes in OOP have been introduced:
    * from PHP 7.0 there is only one reserved keywords: `class` - all previous keywords are now available to use as property, function or constant name
    * PHP 4 constructor is now marked as deprecated
    * we now can write anonymous classes `$object = new class('arg1', 'arg2', ...) { ... }`
21. PHP 5 gave us the ability to type hint but only a specific type of parameters (class, array and callable). In PHP 7.0 we now have the ability to type hint scalar parameters
22. Also return type hinting has been introduced: `function functionName(int param1): array`

This list is only a sneak peek of the changes. I would advice to read whole [PHP 7.0 Migration page](http://php.net/manual/en/migration70.php) to fully understand all changes.

#### :bangbang: Name 5 changes of PHP 7.1 comparing to 7.0  :bangbang:

As in the previous question, there are more than 5 changes between those versions. All changes can be found on the [PHP 7.1 Migration Page](http://php.net/manual/en/migration71.new-features.php)

#####  :sunny: New features
1. Nullable types were introduced - every parameter and return value can be now prefixed with a question mark which means that it can pass `null` values
2. Void return type was introduced - now you can use this syntax `function test($param): void` to specify a function which does not have return statement or uses empty `return;` statement
3. Short array syntax can be used as an alternative to `list()` syntax (as well as within `foreach`) - `[$param1, $param2] = $data` is the same as `list($param1, $param2) = $data`
4. You can now specify visibility of class constants [public, protected, private]:   `private const PRIVATE_CONSTANT = true;`
5. New pseudo-type called `iterable` has been added which accepts arrays and objects implementing `Traversable` interface
6. You can now define multiple exception types in single catch clause by using pipe character: `try { ... } catch (FirstException | OtherException $e) { ... }`
7. Support for keys in `list()` has been added:  `list("id" => $id, "name" => $name) = ["id" => 1,  "name" => "Piotr"];`
8. Support for negative string offsets has been added. You can now write: `var_dump("sampleText"[-1]); // string (1) "t"` and `var_dump(strpos("aabbcc", "b", -3)); // int(3)`
9. Support for AEAD in ext/openssl has been added - [more info](https://wiki.php.net/rfc/openssl_aead)
10. By using new static method of Closure class named `fromCallable()` you can convert callables to closures
11. cURL extension now supports HTTP server push - just pass `CURLMOPT_PUSHFUNCTION` constant by `curl_multi_setopt` function which should be a callable that handles server pushes

##### :sunny: Backward incompatible changes
1. When you pass too few arguments to the function it now throws an Error exception ( before it would emit a warning )
2. It is now forbidden to dynamically call certain functions which could cause unexpected behaviour ( it will now emit a warning )
3. You now can't use `void` and `iterable` keywords as a name of classes, interfaces nor traits
4.  Numerical string conversion now respects scientific notation which basically means that `var_dump((int)"-1.2E2")` will return proper value of `int (-120)` instead of `int(-1)`
5. `mt_rand()` function now uses fixed version of Mersenne Twister algorithm - [read more about the algorithm](http://www.math.sci.hiroshima-u.ac.jp/~m-mat/MT/emt.html)
6. `rand()` and `srand()` functions are now aliases of `mt_rand()` and `md_srand()`
7. There was a bug that allowed to use delete control character (`0x7F`) in identifiers - this is fixed now
8. When you set `error_log` init setting to `syslog` value - all PHP error levels will be mapped to the syslog error levels
9. When objects throw exception in the constructor - their destructor isn't called at all
10. When you call `call_user_func()` with a function name that expects reference as one of the parameter - it will always emit a warning. Despite this, the call will be proceeded as usual
11. You can't use empty index operators to a string (`$str[] = $x;`) - it will throw a fatal error instead of converting string to an array on the fly
12. Ini directives like `session.entropy_file`, `session.entropy_length`, `session.hash_function` and `session.has_bits_per_character` have now been removed

#### :bangbang: What is a trait?  :bangbang:

Traits we introduced in PHP 5.4. Traits, in the term of structure, are similar to classes. They can define sets of methods and properties that 
can be reusable in different classes inside the program structure. 

```php
trait myFirstTrait {
    public function getSomeParam() {  }
    public function getSomeOtherParam() { }
}

class myFirstClass {
    use myFirstTrait;
    /* ... */
}

class mySecondClass {
    use myFirstTrait;
    /* ... */
}

$a = new MyFirstClass();
$b = new MySecondClass();

$a->getSomeParam();  // MyFirstClass inherits this method from myFirstTrait trait
$b->getSomeOtherParam(); // as in the line above method is being inherited from myFirstTrait trait
```

Things you should know about traits:
* traits cannot be instantiated
* precedence order is as follows: members of a current class overrides members of a trait which overrides members of a parent class
* you can insert multiple traits into one class, which should be separated by commas: `use FirstTrait, SecondTrait, ThirdTrait;`
* if there are member names conflicts, use `insteadof` to specify which version of a member to use 
* you can also add an alias for any method by using `as` operator
* by using `as` operator you can also change the visibility of its member: `use MyFirstTrait { myPublicMethod as protected; }`
* you can use traits inside other traits
* you can define abstract methods inside a trait that have to be implemented insite classes that uses this trait
* you can define static members and static methods inside a trait
* last but not least, you can also define properties inside a trait
