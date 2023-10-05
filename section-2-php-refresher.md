---
description: >-
  In this section, we filled in some gaps that will be necessary for learning
  Laravel. Mainly object-oriented programming topics.
---

# Section 2: PHP Refresher

## Section Overview

This lecture does not contain lecture notes.

### Resources

* Replit - [https://replit.com/](https://replit.com/)

## The Command Line

In this lecture, we explored the command line. Before interfaces existed, everything we wanted to do was done through the command line, such as sending emails, downloading files, or playing audio. Developers prefer the command line since a user interface can bog down the performance. Most tools are only executable through the command line.

You can open the command line by searching for a program called **Terminal** on a Windows, Linux, or Mac machine.

There are dozens of commands available. Luckily, it's not required to be a master of the command line. You can get away with the following commands:

* `pwd` - Short for **Present Working Directory**. This command will output the full path you're currently in.
* `ls` - Short for **List**. This command will output a full list of files and folders that are in the current directory.
* `cd` - Short for **Change Directory**. This command will change the current directory. You can use two dots (`..`) to back up a directory instead of moving into a directory.
* `clear` - Clears the command line.

In Visual Studio Code, you can open the command line by going to **Terminal > New Terminal**. By default, the command line will point to your project directory, which can make things easier. This saves you time from moving the command line to your project.

## Running PHP in the Command Line

In this lecture, we learned how to execute a PHP file from the command line. Before being able to do so, PHP must be installed globally on your system. Using a program like WAMP or XAMPP does not mean PHP is installed globally as these programs isolate PHP.

After confirming PHP is installed, you can use the `php`command followed by the filename to execute like so:

```
php some-file.php
```

## What is OOP (Object-Oriented Programming)?

In this lecture, we talked about programming paradigms and how they apply to OOP. There are no notes for this lecture.

## Classes

In this lecture, we learned about classes. Classes are blueprints for creating objects. An object can be anything we want. We can use an object to represent a UI element or a database entry.

Classes can be defined with the `class` keyword.

```php
class Account {

}
```

It's standard practice to name your class after the name of your file and to use pascalcasing.

Since classes are just blueprints, we can't interact with the data inside of a class until it has been instantiated. Instantiation is the process of creating an object from a class. We can instantiate a class using the `new` keyword like so.

```php
$myAccount = new Account;
$johnsAccount = new Account;
```

We can even create multiple instances.

## Properties

In this lecture, we talked about properties, which are variables defined inside a class. We must define a property by using an access modifier followed by the name of the variable.

```php
class Account {
  public $name;
  public $balance;
}
```

An access modifier determines how accessible the property is outside of the class. The `public` keyword allows for a property to be updated anywhere from our script.

We can access the property using the `->` from the respective instance.

```php
$myAccount = new Account;

$myAccount->balance = 10;

var_dump($myAccount->balance);
```

We can set properties to any type of value, but we can't use complex operations, such as setting a property to a function.

```php
public float $balance = intval(5.5); // Not allowed
```

### Resources

* [Access Modifiers](https://www.php.net/manual/en/language.oop5.visibility.php)

## Magic Methods

In this lecture, we learned about magic methods. A method is the terminology for a function defined inside a class. Magic methods are functions defined inside a class that is automatically called by PHP.

There are various magic methods available, but the most common method is `__construct()`. Most magic methods begin with two `_` characters. It's recommended to avoid using two `_` characters in your own methods to reduce confusion.

```php
class Account
{
  public string $name;
  public float $balance;

  public function __construct(
    string $newName,
    float $newBalance
  ) {
    $this->name = $newName;
    $this->balance = $newBalance;
  }
}
```

In this example, the `__construct()` method has the `public` access modifier. This allows for our method to be accessible anywhere. Whenever we create a new instance of the `Account` class, the `__construct()` method gets called.

We can pass on data to this method like so.

```php
$myAccount = new Account("John", 100);
```

### Resources

* [Magic Methods](https://www.php.net/manual/en/language.oop5.magic.php)

## Constructor Property Promotion

In this lecture, we learned of a shorter way of defining properties and setting their values from within a `__construct()` method. If we add the access modifier to the parameter, PHP will automatically treat the parameter as a class property and set the value passed into the method as the value for the respective parameter.

The solution from the previous lecture can be shortened to this:

```php
class Account
{
  public function __construct(
    public string $name,
    public float $balance
  ) { }
}
```

It'll result in the same behavior as before.

## Custom Methods

In this lecture, we learned how to define a custom method in a class. One of the benefits of using a method in a class is the ability to access the current instance's properties. For example, take the following:

```php
class Account
{
  public function __construct(
    public string $name,
    public float $balance
  ) { }

  public function deposit(float $amount) {
    $this->balance += $amount;
  }
}
```

In this example, we have a method called `deposit()`. This method updates the `$balance` property via the `$this` keyword. As you can see, we never have to worry about updating the incorrect property. Methods have access to the property values of the current instance.

In addition, we can return the current instance from our methods to allow method chaining. For example, let's say we updated the `deposit()` method to this:

```php
public function deposit(float $amount) {
  $this->balance += $amount;

  return $this;
}
```

Returning the `$this` keyword allows us to chain methods like so:

```php
$myAccount = new Account('John', 20);

$myAccount->deposit(50)->deposit(30);
```

## Taking on Exercises

In this lecture, we talked about how to tackle exercises on Udemy. There are no notes for this lecture.&#x20;

## Exercise: Instantiating Classes

Here's the solution to this exercise:

```php
<?php

class Student {
    public $name;
    
    public function __construct($newName) {
        $this->name = $newName;
    }
    
    public function getNameInUppercase() {
        return strtoupper($this->name);
    }
}
```

## Understanding Namespaces

In this lecture, we talked about namespaces. There are no notes for this lecture.

## Creating a Namespace

In this lecture, we created a namespace by using the `namespace` keyword. Following this keyword, we must provide a name. Namespaces follow the same naming rules for classes or functions. Generally, most developers use pascalcasing for namespaces.

```php
namespace App;

class Account {
  // Some code here...
}
```

We can access a class from within a namespace by typing the namespace and class like so.

```php
$myAccount = new App\Account();
```

However, you may not want to type out the entire path. You can use the `use` keyword to import a class from a namespace. This will allow you to create an instance with just the class name.

```php
use App\Account;

$myAccount = new Account();
```

## Working with Namespaces

In this lecture, we went over various things to be aware of when using namespaces. Firstly, it's common practice for the namespace to mimick a project's directory. For example, if a class exists in a folder called `App`. The namespace should be called `App`. Not required but recommended to make it easier to find classes.

The second thing to be aware of is that we don't need to use the `use` statement or type out the complete namespace when classes exist in the same namespace.

Another thing to know is that PHP will only resolve classes to the current namespace. For example, let's say we wanted to use a class called `DateTime` from a file in the `App` namespace.

```php
new DateTime();
```

PHP will throw an error because it'll attempt to look for the class with the following path: `App\DateTime`. In order to use a class from a different namespace, such as the global namespace, we must add the `\` character before the classname like so.

```php
new \DateTime();
```

Alternatively, we can import the class with the `use` keyword without the `\` character.

```php
use DateTime;

new DateTime();
```

It's important that the `use` statement to be in the same file as where we're using the class. The `use` statement only applies to the current file.

Lastly, we can add aliases for classes with the `as` keyword.

```php
use DateTime as DT;

new DT();
```

### Resources

* [Name Resolution Rules](https://www.php.net/manual/en/language.namespaces.rules.php)
* [Namespace FAQ](https://www.php.net/manual/en/language.namespaces.faq.php)

## Autoloading Classes

In this lecture, we learned how to automate the process of loading PHP files with classes. There's a function called `spl_autoload_register()` that we can call for intercepting classes that are used in a program, but haven't been defined.

We can pass in a function that will be responsible for loading a specific class, which is passed on to our function as a parameter.

```php
spl_autoload_register(function($class) {
  $formattedClass = str_replace("\\", "/", $class);
  $path = "{$formattedClass}.php";
  require $path;
});
```

In the above example, the first thing we're doing is replacing the `\` character with a `/` character since the `require` statement does not allow `\` characters. To accomplish this, we're using the `str_replace()` function, which accepts the string to search for in a given string, the string to replace it with, and the string to search.

In the first argument, we're escaping the `\` character by using `\\` since the `\` character escapes a string. Escaping a string is the process of telling PHP not to close the string with the closing double-quote.

Next, we created a variable called `$path`, which contains the path to the file that contains the class. Lastly, we use the `require` keyword to load the file.

## Using Constants in Classes

In this lecture, we used a constant in a class. Classes do not support the `define()` function for constants. We must use the `const` keyword like so.

```php
class Account {
  public const INTEREST_RATE = 2;
}
```

Next, we can access a constant by using the scope resolution operator (`::`).

```php
Account::INTEREST_RATE;
```

Alternatively, you can also access a constant from an instance of a class.

```php
$myAccount = new Account();
$myAccount::INTEREST_RATE;
```

## Static Properties and Methods

In this lecture, we learned how to use static properties and methods. Static properties are similar to constants, except they can have their values modified. We can define a static property with the `static` keyword. This keyword can be positioned before or after an access modifier.

```php
class Account {
  public static int $count = 0;
}
```

We can access the static property like so.

```php
Account::$count;
```

Alternatively, you can also access a static property from an instance of a class.

```php
$myAccount = new Account();
$myAccount::$count;
```

Typically, static properties are avoided since they can be altered anywhere, just like global variables. On the other hand, static methods are popular as a means of creating utility methods. Take the following:

```php
class Utility {
  public static function printArray(array $array) {
    echo '<pre>';
    print_r($array);
    echo '</pre>';
  }
}
```

Since the method is static, we can invoke the method without requiring an instance like so.

```php
Utility::printArray([1, 2, 3]);
```

## Exercise: Static Classes

Here's the solution to this exercise:

```php
<?php

namespace App;

class Allergies {
    public static $items = [];
    
    public static function getItems() {
        return implode(",", self::$items);
    }
}
```

## Encapsulation

In this lecture, we learned about an object-oriented programming principle called encapsulation. Encapsulation is the idea of restricting data and methods to a single class.

In your classes, you can prevent outside sources from modifying properties by using the `private` access modifier.

```php
public function __construct(
  private string $name,
  private float $balance
) { }
```

By changing the modifier to `private`, only the current class can modify a given property.

But what if we want to read or update the property? In this case, we can create getter or setter methods, which are just methods that can be used for accessing a specific property. Here's an example of a getter.

```php
public function getBalance() {
  return "$" . $this->balance;
}
```

It's common practice to set the name of the method to the word "get" followed by the name of the property to grab. One of the main benefits of getters is being able to format values before returning them.

As for setters, they're methods for updating a property. It's standard practice to set the name to the word "set" followed by the name of the property.

```php
public function setBalance(float $newBalance) {
  if ($newBalance < 0) return;

  $this->balance = $newBalance;
}
```

The main benefit of setters is that we can validate data before updating a property. Overall, getters and setters give us more power over how our properties are read and set.

We're not limited to private properties. Methods can be private too. This can be useful when you want to subdivide a method into multiple actions without exposing a method outside of a class.

```php
public function setBalance(float $newBalance) {
  if ($newBalance < 0) return;

  $this->balance = $newBalance;
  $this->sendEmail();
}

private function sendEmail() {}
```

In the following example, the `sendEmail()` method is private, which will be responsible for sending an email to the user if the balance is successfully updated.

## Abstraction

In this lecture, we talked about the idea of abstraction. Abstraction is the idea of hiding complexities away into a method so that outside sources don't have to worry about them. Most people know how to use coffee machines or cars, but they don't know the inner mechanisms of these machines. Regardless, they're still able to use them.

This idea can be applied to programming. We can define classes to perform complex actions and then use them elsewhere without having to understand the complete implementation details of a class's methods.

## Inheritance

In this lecture, we learned about inheritance. The idea of inheritance is that a class can be derived from another class. Properties and methods from the parent class will be available in the child class as its own properties and methods.

Take the following:

```php
class Toaster {
  public int $slots = 2;

  public function toast() {
    echo "toasting bread";
  }
}

class ToasterPremium {
  public int $slots = 4;

  public function toast() {
    echo "toasting bread";
  }
}
```

In this example, we have two classes with the same property and method, which is redundant. To reduce the amount of code you can write, you can use the `extends` keyword for a class to inherit properties and methods from another class.

```php
class Toaster {
  public int $slots = 2;

  public function toast() {
    echo "toasting bread";
  }
}

class ToasterPremium extends Toaster {
  public int $slots = 4;
}
```

In the above example, the `ToasterPremium` class inherits from the `Toaster` class. Therefore, it's not necessary to add the `toast()` method again.

In addition, if we want to override properties or methods from the parent class, we're allowed to do so. PHP prioritizes the child class properties and methods over the parent.

One thing to keep in mind is that the `$this` keyword points to the current instance, even if it's being used in the parent class.

## Protected Modifier

In this lecture, we learned about the protected modifier. PHP allows you to override properties, but if a property is `private`, child classes won't be able to change the value of a parent class. You can get the best of public and private properties by using the `protected` modifier.

The `protected` modifier allows child classes to modify parent properties but prevent code outside of a class from changing the property value.

```php
protected int $balance = 5;
```

## Interfaces

In this lecture, we learned how to use interfaces, which are a feature in PHP for defining how a class should be implemented. Interfaces can contain method definitions that should be implemented by a class. We can create an interface with the `interface` keyword.

```php
interface RestaurantInterface {
  public function prepareFood();
}
```

It's common practice to add the word "Interface" to the name. Alternatively, you can begin the name with the capital letter "I." This would produce an interface name such as `IRestaurant`. Either naming convention is valid.

A few things to know about interfaces.

1. Properties are not allowed
2. Methods must be public
3. Methods are automatically abstract.
4. Constants are supported

We can apply an interface to a class by adding the `implements` keyword to the class. Multiple interfaces can be added to a class by separating them with a comma.

```php
class RestaurantOne implements RestaurantInterface {
  public function prepareFood() {
    echo "preparing food";
  }
}
```

## Anonymous Classes

In this lecture, we learned about anonymous classes, which are just classes that don't have a name. For example, let's say we wanted to pass an anonymous class to the `FoodApp` class. We can do so with the following code:

```php
$restaurant = new FoodApp(new class implements RestaurantInterface {
  public function prepareFood() {
    echo "{$this->name} preparing food";
  }
});
```

Similar to regular classes, anonymous classes support interfaces, inheritance, methods, and properties. What if we want to pass on data to a `__construct()` method? We can do so by adding the argument list after the `class` keyword like so.

```php
$restaurant = new FoodApp(new class("popup restaurant") implements RestaurantInterface {
  public function __construct(
    public string $name
  ) {}

  public function prepareFood() {
    echo "{$this->name} preparing food";
  }
});
```

## Throwing Exceptions

In this lecture, we learned how to throw an exception from PHP. We can use the `throw` keyword followed by a new instance of the `Exception` class.

```php
throw new \Exception("Some error message");
```

The `Exception` class will format your message in the output along with the filename, line number, and other pieces of information related to the error. PHP has other classes for throwing exceptions, you can refer to the resource section for a list of them.

For example, we can use the `InvalidArgumentException` class for arguments that are invalid for a method call.

```php
throw new \InvalidArgumentException("Some error message");
```

Why do we say throw an exception? Because it implies that an exception can be caught and can be handled for a more custom experience, such as redirecting the user instead of completely stopping the script.

#### Resources

* [List of Exception Classes](https://www.php.net/manual/en/spl.exceptions.php)

## Custom Exceptions

In this lecture, we learned how to create a custom exception class instead of using PHP's exception classes. Custom exceptions can be created to customize the errors thrown by our script. All exceptions derive from the `Exception` class. So, all you have to do is create a class that extends the `Exception` class.

```php
class EmptyArrayException extends \Exception {
  protected $message = "Array is empty";
}
```

You can override any of the properties from the class. Check out the resource section for a link to the `Exception` class for a complete list of properties.

You can use the new exception like so.

```php
throw new EmptyArrayException();
```

#### Resources

* [Exception Class](https://www.php.net/manual/en/class.exception.php)

## Catching Exceptions

In this lecture, we learned how to catch an exception by using the `try catch` statement. If we want to catch errors, we must surround the code with the `try` block.

```php
try {
  Utility::printArray([]);
}
```

Next, we must provide a `catch` block.

```php
try {
  Utility::printArray([]);
} catch(EmptyArrayException|InvalidArgumentException $e) {
  echo "Custom Exception: {$e->getMessage()} <br />";
} catch (Exception $e) {
  echo "Default Exception: {$e->getMessage()} <br />";
}
```

In the `catch` block's parameter list, we can accept the error that was thrown. In addition, if we add the type, we can apply the `catch` block to specific exceptions. Multiple exceptions can be handled by a single `catch` block by separating them with a `|` character.

If we want to handle all exceptions, we can add a `catch` block where the `$e` parameter is `Exception` since all exceptions derive from this class.

Lastly, we can add the `finally` block that will be executed regardless if an error gets thrown or not.

```php
try {
  Utility::printArray([]);
} catch(EmptyArrayException|InvalidArgumentException $e) {
  echo "Custom Exception: {$e->getMessage()} <br />";
} catch (Exception $e) {
  echo "Default Exception: {$e->getMessage()} <br />";
} finally {
  echo "Finally block <br />";
}
```

## Exercise: Inheritance

Here's the solution to this exercise:

```php
<?php

require_once "Vehicle.php";
require_once "DriveInterface.php";

class Car extends Vehicle implements DriveInterface {
    public function drive() {
        $this->speed = 40;
    }
}
```
