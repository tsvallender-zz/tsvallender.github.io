---
title: Ruby
stub: post
layout: post
desc: An introduction and overview of Ruby
author: T S Vallender
date: 2022-01-19
---

This is my overview of Ruby, aiming to give a bird’s eye view of the
language. My goal is to present information in such a way that it will
prove as a useful introduction to Ruby for programmers coming from
other languages, and as a reference for relatively new Ruby
developers. It is not an introduction to programming, nor is it in any
way exhaustive. It should be used as a place to jump off from and dive
deeper through other sources whenever you reach an area you wish to
know more about.

## Variables

### Setting variables

{% highlight ruby %}
name = "T S Vallender"
{% endhighlight %}

### Types

There is no need to declare a variable’s type.

#### Numbers

##### Operators

{% highlight ruby %}
5 + 5 # 10
5 - 2 # 3
5 * 5 # 25
10 / 5 # 2
3 ** 3 # 27 (Exponent)
10 % 5 # 0 (Modulo)
{% endhighlight %}

Ruby uses standard mathematical order of operation (PEDMAS/BODMAS).

##### Numeric types

Floats are an imprecise data type due to the way they are stored and
decimal should be used when precision is necessary. Rational is also
available for dealing with rational numbers, but care must be taken
not to treat an irrational number as rational.

{% highlight ruby %}

0.2 + 0.1 == 0.3 # false due to float imprecision
BigDecimal("0.2") + BigDecimal("0.1") == 0.3 # true
{% endhighlight %}

#### Strings

Strings are defined between double or single quotes. Doubles allow for
string interpolation, singles do not.

##### String interpolation

{% highlight ruby %}
puts "I can insert #{my_var} into a string"
{% endhighlight %}

Any valid Ruby can be interpolated, often used to give an optional
default value with a conditional.

##### String manipulation

Some common string manipulation methods:

{% highlight ruby %}
name = "T S Vallender"
name.upcase # "T S VALLENDER"
name.downcase # "t s vallender"
name.reverse # "rednellaV S T"

poem = "And the Raven, never flitting, still is sitting, still is sitting"
poem.sub "sitting", "standing"
# "And the Raven, never flitting, still is standing, still is sitting
poem.gsub "sitting", "standing" # "And the Raven, never flitting, still is standing, still is standing
# Note these do not change the original value - you need sub! and gsub! for that.

quote = "  Quoth the Raven “Nevermore.   "
quote.strip! "Quoth the Raven “Nevermore."
quote.split # ["Quoth", "the", "Raven", "Nevermore"]
{% endhighlight %}

#### Arrays

Arrays are an <code>Enumerable</code> type.

{% highlight ruby %}
arr = [3, 'Three', 8, 3, true]
arr.delete 3 # ['Three', 8, true]
arr.delete_at 0 # [8, true]

fellowship = ['Gimli', 'Pippin', 'Aragorn', 'Frodo', 'Pippin' ]
fellowship.delete_if { |x| x.length > 5 }
# ['Gimli', 'Aragorn']
fellowship.join(' and ') # "Gimli and Aragorn"
{% endhighlight %}

Items can be pushed to an popped from arrays with <code>.push</code>
and <code>.pop</code>. <code>.pop</code> returns the value popped.

<code>nil</code> values are added to any empty spaces in an array.

Arrays of strings can also be declred using the below syntax

{% highlight ruby %}
arr = %w(One Two Three Four)
{% endhighlight %}

##### Common methods

{% highlight ruby %}
arr = ["a", "b", "c"]
arr.size # 3
{% endhighlight %}

#### Hashes

Hashes are another <code>Enumerable</code> type. They are a key: value
collection.

{% highlight ruby %}
fellowship = { boromir: "Human", gimli: "Dwarf", legolas: "Elf", aragorn: "Human", frodo: "Hobbit" }
fellowship[:gimli] # "Dwarf"
fellowship.delete :boromir
fellowship.each_key { |x| puts x }
fellowship.each_value { |x| puts x }

fellowship[:gandalf] = 'Maiar' # add a new key-value pair.
fellowship.invert # flips keys and values

more = { pippin: "Hobbit", merry: "Hobbit", sam: "Hobbit" }
fellowship.merge more # combine hashes

fellowship.keys # array of keys
fellowship.values # array of values
{% endhighlight %}

This is the modern syntax. Ruby converts these internally to
symbols. Older syntaxes include <code>{ "gimli" => "Dwarf" }</code> and
<code>{ :gimli => "Dwarf" }</code>.

### Scope

<dl>
  <dt>Local variables</dt>
  <dd>Local variables are limited to the scope in which they are declared
  (e.g. a method or loop).</dd>

  <dt>Global variables</dt>
  <dd>Global variables are defined with a leading $. They are generally a
  bad idea.</dd>

  <dt>Instance variables</dt>
  <dd>Instance variables are defined with a leading @ and are available to
  a given instance of a given object.</dd>

  <dt>Class variables</dt>
  <dd>A class variables are defined with two leading @s and are available
  to all instances of a class. They are rarely used.</dd>

  <dt>Constants</dt>
  <dd>Constants are defined with an initial capital (generally in all caps.
  They *can be changed*, Ruby will just issue a warning if you do so.</dd>
</dl>

## Conditionals

Ruby supports the standard conditional operators <code>==, !=, <, >,
<= and <=</code>.

Compound conditionals are supported with <code>&&</code> and
<code>||</code>. Priority can be enforced with parentheses. Ruby also
gives <code>and</code> and <code>or</code>, which have lower
precendence.

{% highlight ruby %}
if x < y
  puts "#{x} is bigger"
elsif x > y
  puts "#{y} is bigger"
else
  puts "They are equal!"
end

# conditionals can also go on the end:

puts "They are equal" if x == y

arr = [1, 2, 3]
unless arr.empty?
  puts arr
end

puts arr unless arr.empty?

## Ruby also supports the ternary operator
x = y > z ? y : z # sets x to the larger of y or z
{% endhighlight %}

## Iterators & Loops

### While

{% highlight ruby %}
while true
  p "Infinite loop"
end
{% endhighlight %}

### Each

The <code>each</code> method is available on any collection of items

{% highlight ruby %}
[1, 2, 3].each do |x|
  p x # x is the element
end

[1, 2, 3].each { |x| p i } # equivalent to above

# If an index is required:

[1, 2, 3].each_with_index do | x, i |
  p "Index: ", i, "Value: ", x
end
{% endhighlight %}

With a hash, <code>.each</code> use:
{% highlight ruby %}
my_hash.each do |key, value|
  p key, value 
end
{% endhighlight %}

### For in

Rarely used, <code>.each</code> is more common.

{% highlight ruby %}
for i in 0..10
  p i # prints 0 to 10
end
{% endhighlight%}

## Methods

{% highlight ruby %}
def my_method
  puts "This is my method"
end
{% endhighlight %}

Methods in Ruby return the value of their final
statement. <code>return</code> is generally only used to return early.

### Naming methods

Methods are generally defined in <code>snake_case</code>.

Methods with a trailing ! are "dangerous", such as those in the core
usually modifies its receiver.

### Class vs. instance methods

Class methods are defined with a leading <code>self.</code>. Instance
methods can only be called on an instance of a class.

### Arguments

{% highlight ruby %}
def say_hello(name)
  puts "Hello #{name}!"
end

say_hello("Trevor") # "Hello Trevor!"
{% endhighlight %}

Parentheses are optional both when defining the function and calling it:
{% highlight ruby %}
def say_hello name
  puts "Hello #{name}!"
end

say_hello "Trevor" # "Hello Trevor!"
{% endhighlight %}

#### Named arguments
{% highlight ruby %}
def say_hello name:, place:
  puts "Hello #{name} in #{place}!"
end

say_hello name: "Trevor", place: "UK" # Hello Trevor in UK
{% endhighlight %}

#### Default arguments
{% highlight ruby %}
def say_hello name:, place: "UK"
  puts "Hello #{name} in #{place}!"
end

say_hello name: "Trevor" # Hello Trevor in UK
{% endhighlight %}

#### Collections as arguments

A *splat* argument allows multiple arguments to be treated as an array.

{% highlight ruby %}
def make_array *species
  species
end

make_array "Dwarf", "Elf", "Halfling" # [ "Dwarf", "Elf", "Halfling"]
{% endhighlight %}

A keyword-based splat argument takes a hash value instead
{% highlight ruby %}
def identify **characters
  characters.each do |species, name|
    puts "#{name} is a #{species}
  end
end

c = { "Dwarf": "Gimli", "Elf": "Legolas" }
identify c
# Gimli is a Dwarf
# Legolas is a Elf
{% endhighlight %}

#### Optional arguments

Optional arguments use an empty <code>options</code> hash.

{% highlight ruby %}
def stats options={}
  puts options[:optional]
end

stats optional: "HEY!"
{% endhighlight %}

## Procs and Lambdas

Procs and lambdas are encapsulations of a piece of code in a variable.

Procs and lambdas are *closures* and thus remember they retain the
context in which they were created.

### Procs
{% highlight ruby %}
my_proc = Proc.new { |x| x ** x }
my_equiv_proc = proc { |x| x ** x }
another_equiv_proc = Proc.new do |x|
  x ** x
end

my_proc.call(3) # 27
my_proc.(3) # 27
my_proc[3] # 27
{% endhighlight %}

### Lambdas

{% highlight ruby %}
my_lambda = lambda { |x| x ** x }
my_lambda[3] # 27

# "Stabby lambda" syntax:
my_equiv_lambda = ->(x) { x ** x}
{% endhighlight %}

### Differences

* Lambdas count the number of arguments they are given, and will raise
  an error with the wrong number. Procs will ignore superfluous ones.
* <code>return</code> in a lambda only returns from the lambda,
  <code>return</code> from a proc will return from the calling method.

## Enumerators

### Select

Select returns those elements of a collection which meet a given criteria.

{% highlight ruby %}
(1..20).to_a.select { |x| x.even? }
(1..20).to_a.select(&:even?) # equivalent
{% endhighlight %}

### Map

Map takes a collection and performs an operation on each one of its members.

{% highlight ruby %}
arr = ["1", "2", "10"]
arr.map(&:to_i) # [1, 2, 3]
{% endhighlight %}

This can be used to create a hash of a value with an associated value,
for example strings with their length:

{% highlight ruby %}
arr = %w(Aragorn, Frodo, Gimli, Gandalf)
Hash[arr.map { |x| [x, x.length] }]
{% endhighlight %}

### Inject/Reduce

Inject and reduce are aliases. They combine a collection by the
repeated application of a binary operator. For example, to sum all
elements of an array:

{% highlight ruby %}
[4, 3, 6, 2].reduce(&:+) # 15
{% endhighlight %}

If passed a code block, each element in the enumerable object is
passed an accumulator and the element.

{% highlight ruby %}
[fellowship = ['Gimli', 'Pippin', 'Aragorn', 'Frodo' ]

fellowship.inject do | longest, current |
  current.length &gt; longest.length ? current : longest
end

# Aragorn
{% endhighlight %}

## Symbols

A symbol is a number with an attached identifier, which is a series of
characters or bytes. They are represented in Ruby with a leading
colon.

Symbols should be used whenever a textual representation of a discrete
set of options is required. If you are dealing with more freeform
text, use strings.

Ruby will often convert between symbols and strings for the
programmer's convenience. If possible, you should supply the correct
type initially, however, for the best performance.

## Working at the console

### Writing to the console

{% highlight ruby %}
puts name # returns nil
p name # returns value
{% endhighlight %}

Note also that <code>puts</code> will pretty-print, while
<code>p</code> will print arrays including commas, brackets etc.,
strings wrapped in quotation marks and is thus generally less suitable
for use with end users.

### Receiving input at the console

{% highlight ruby %}
name = gets.chomp # chomp removes trailing newline
{% endhighlight %}

## Object-oriented Ruby

Everything in Ruby is an object.

Classes are named with CamelCase.

{% highlight ruby %}
class Humanoid
  attr_accessor :name, :address # creates getters and setters
  # initializer method run when new objects are created
  def initialize name:, address:
    @name = name
    @address = address
  end

  def location
    puts "#{name} lives in #{address}"
  end

  def self.fact # Class method
    puts "Humanoids have two legs"
  end
end

class Hobbit &lt; Humanoid
  def initialize name:, address: "The Shire"
    super # Calls parent method
  end
  
  def self.fact
    puts "Hobbits have hairy feet"
  end
end

bilbo = Hobbit.new name: 'Bilbo'
p bilbo.name, bilbo.address
bilbo.location
Hobbit.fact
aragorn = Humanoid.new name: "Strider", address: "Gondor"
Humanoid.fact
{% endhighlight %}

Methods below a <code>private</code> keyword are only accessible from
the given class. Note there are ways around this but doing so is bad
practice. Protected methods are also unavailable outside the class,
but while within that class may be called on objects. They are
uncommon and private should be used where possible.

## The filesystem

{% highlight ruby %}
f = File.new '/path', 'w+'
f.puts "contents"
f.close

File.open '/path', 'w+' do |f| # second option is mode 
  f.puts("contents")
end

File.write '/path', "contents"

content = File.read '/path' # reads as string

File.delete '/path'

{% endhighlight %}

## Errors

{% highlight ruby %}
begin
  puts 10 / 0
rescue ZeroDivisionError => e
  puts e
end
{% endhighlight %}

Note you should deal with the error in the initial <code>begin</code>
block, <code>rescue</code> should only be for dealing with the error
object itself.

