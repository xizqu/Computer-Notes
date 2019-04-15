# Language

Ruby was made in 1990

# Variables

```ruby
"String"                # Mutable
:symbol                 # Immuatable (Not 100% accurate but just think immutable)
Number
[A, R, R, A, Y]         # Mutable
{this: "is", a: "Hash"} # Mutable
CONSTANT                # Muatable but should be treated as immutable (hence why its a constant)
$Global                 # Immutable
@@Classs                # Immutable
@Instance               
```

## Strings
```ruby
"The man said, 'Hi there!'"

# Ex 2: with single quotes and escaping
'The man said, \'Hi there!\''
```
The backslash, or escape (\) character, tells the computer that the quotes that follow it are not meant as Ruby syntax but only as simple quote characters to be included in the string.

## Symbols

Basically, a symbol is used when you want to reference something like a string but don't ever intend to print it to the screen or change it. It is often referred to as an immutable (i.e. unchangeable) string. While not 100% technically correct, it is a useful mnemonic device for now.

```ruby
:sym = 10
```

## Numbers

Numbers are represented many ways in Ruby. The most basic form of a number is called an integer. It is represented by the whole number only, with no decimal point. A more complex form of a number is called a float. A float is a number that contains a decimal.

```ruby
# Example of integers
1, 2, 3, 50, 10, 4345098098

# Example of floats
1.2345, 2345.4267, 98.2234
```

## Arrays

## Hashes

```ruby
h = {key: "value" this: "is", a: "Hash"}
```

## Constants

Constants are declared by capitalizing every letter in the variable's name. They are used for storing data that never needs to change. While most programming languages do not allow you to change the value assigned to a constant, Ruby does. It will however throw a warning letting you know that there was a previous definition for that variable. Just because you can, doesn't mean you should change the value. In fact, you should not. Constants cannot be declared in method definitions, and are available throughout your application's scopes.

```ruby
MY_CONSTANT = 'I am available throughout your app.'
```

## Global Variables

Global variables are declared by starting the variable name with the dollar sign ($). These variables are available throughout your entire app, overriding all scope boundaries. Rubyists tend to stay away from global variables as there can be unexpected complications when using them.

```ruby
$var = 'I am also available throughout your app.'
```

## Class Variables

Class variables are declared by starting the variable name with two @ signs. These variables are accessible by instances of your class, as well as the class itself. When you need to declare a variable that is related to a class, but each instance of that class does not need its own value for this variable, you use a class variable. Class variables must be initialized at the class level, outside of any method definitions. They can then be altered using class or instance method definitions.

```ruby
@@instances = 0
```

## Instance Variables

Instance variables are declared by starting the variable name with one @ sign. These variables are available throughout the current instance of the parent class. Instance variables can cross some scope boundaries, but not all of them. 

```ruby
@var = 'I am available throughout the current instance of this class.'
```

# Methods

You'll often have a piece of code that needs to be executed many times in a program. Instead of writing that piece of code over and over, there's a feature in most programming languages called a procedure, which allows you to extract the common code to one place. In Ruby, we call it a **method**.

```ruby
def say(words)
  puts words
end

say("hello")
say("hi")
say("how are you")
say("I'm fine")
```

You'll notice that there's a ```(words)``` after ```say``` in the method definition. This is what's called a parameter. Parameters are used when you have data outside of a method definition's scope, but you need access to it within the method definition.

## Default Parameters

Default Parameters
When you're defining methods you may want to structure your method definition so that it always works, whether given parameters or not. Let's restructure our say method definition again so that we can assign a default parameter in case the caller doesn't send any arguments.

```ruby
say.rb
def say(words='hello')
  puts words + '.'
end

say()
say("hi")
say("how are you")
say("I'm fine")
You'll notice that say() prints hello. to the console. We have provided a default parameter that is used whenever our method is called without any arguments. Nice!
```

Say() could be rewritten as just say. With arguments, instead of say("hi"), it could just be say "hi". This leads to more fluid reading of code, but sometimes it can be confusing. Keep that in mind when you're reading Ruby; it can get tricky deciphering between local variables and method names!

# Scope

## Variable Scope

A variable's scope determines where in a program a variable is available for use. A variable's scope is defined by where the variable is initialized or created. 

In Ruby, variable scope is defined by a block.

**Inner scope can access variables initialized in an outer scope, but not vice versa.**

```ruby
# scope.rb

a = 5

3.times do |n|    # method invocation with a block
  a = 3           # a is available here 
  b = 5           # b is initialized in the inner scope
end

puts a
puts b            # b is not accessible and will cause an error
```

for...do/end code does not create a new inner scope, since for is part of Ruby language and not a method invocation. When we use .each, .times and other method invocations, followed by {} or do/end, that's when a new block is created.

## Method Scope

A method definition creates its own scope outside the regular flow of execution.

```ruby
a = 5            # Lets call this object 1

def some_method
  a = 3          # This is will be object 2 as it has a different location in memory
end

puts a           # This will output object 1 which equals 5
```
Make sure you don't mix up **method invocation** with a block and **method definition** when you're working with local variable scope issues.

```ruby
# Method invocation with a block

[1, 2, 3].each do |num|
  puts num
end
# Method definition

def print_num(num)
  puts num
end
```

## Mutating The Caller

Sometimes, when calling a method, the argument can be altered permanently. We call this mutating the caller.

```ruby
a = [1, 2, 3]

# Example of a method definition that modifies its argument permanently
def mutate(array)
  array.pop
end

p "Before mutate method: #{a}"
mutate(a)
p "After mutate method: #{a}"
```

How do you know which methods mutate the caller and which ones don't? Unfortunately, you have to memorize it by looking at the documentation or through repetition.
 
## Return

Every method returns the evaluated result of the last line that is executed.

```ruby
a = [1, 2, 3]

def mutate(array)
  array.pop
end

p "Before mutate method: #{a}"
p mutate(a)
p "After mutate method: #{a}"

# Output
"Before mutate method: [1, 2, 3]"
3
"After mutate method: [1, 2]"
```

# Useful

## Truthy / Falsy

Everything in ruby is truthy except false and nil