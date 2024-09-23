# Ruby

## Presentation

Installation:
```
sudo apt install ruby
```

Get the version of Ruby:
```
ruby -v
```

Run an Interactive Ruby (IRB):
```
irb
```

Clean the console:
```
CTRL + L
```

Exit the console:
```
quit OR exit
```

Run a ruby script:
```
ruby mon_script.rb
```

Library Ruby:
```
gem
```

## Syntax

### Types

#### Integer

Definition:
```
> int = 1
=> 1
```

#### String

Definition:
```
> string = "text"
=> text
```

#### Boolean

Definition:
```
> bool = true
=> true
```

Example, file.rb:
```rb
a = 15
bool = (a > 10)
puts bool
```

Run:
```
> ruby file.rb
true
```

### Operator

```
+=
```

### Array

Definition:
```
> tab = [1,2,4]
=> [1, 2, 4]
```

Get element:
```
> tab[2]
=> 4
```

Get size:
```
> tab.size
=> 3
```

Reverse:
```
> tab.reverse
=> [4, 2, 1]
```

Add element at the end:
```
> tab << 8
=> [1, 2, 4, 8]
```

### Hash

Definition:
```
> hash = {a:1, b:2}
=> {:a=>1, :b=>2}
```

Get element:
```
> hash[:a]
=> 1
```

Add element:
```
> hash[:c] = 3
=> 3
```

Show hash:
```
> hash
=> {:a=>1, :b=>2, :c=>3}
```

### Loop

#### Example 1

file.rb:
```rb
tab = [1, 2, 3]

tab.each do |i|
    puts i
end
```

Run:
```
> ruby file.rb
1
2
3
```

####Example 2

file.rb:
```rb
3.times do
    puts "Hello"
end
```

Run:
```
> ruby file.rb
Hello
Hello
Hello
```

#### Example 3

file.rb:
```rb
3.times do |i|
    puts "Hello #{i}"
end
```

Run:
```
> ruby file.rb
Hello 0
Hello 1
Hello 2
```

### Condition

#### Syntax

```
==    equal to
!=    not equal to
>     greater than
<     lower than
>=    greater or egal than
<=    lower or egal than
&&    logical and
||    logical or
```
```
if
elsif
else
end
```

#### Example 1

file.rb:
```rb
a = 5

puts "a = #{a}"

if a > 10
    puts "a > 10"
else
    puts "a <= 10"
end
```

Run:
```
> ruby file.rb
a = 5
a <= 10
```

### Class

#### Syntax

To create a class:
```rb
class <Name>
    ...
end
```

/!\ The class name must start with a capital letter.

#### Attribute

```rb
    attr_accessor :<attr_1>, :<attr_2>
```

#### Method initialize

Method call when a new object is created.
```rb
    def initialize(<parameter>)
        <method_definition>
    end
```

#### Method

```rb
    def <method>
        <method_definition>
    end
```

#### Method with parameter

```rb
    def <method>(<parameter>)
        <method_definition>
    end
```

#### Heritage

```
class <Name> < <Class_parent>
    ...
end
```


#### Example 1

file.rb:
```rb
class Utilisateur
    attr_accessor :prenom, :nom, :pays

    def initialize(prenom)
       @prenom = prenom
    end

    def nom_complet
        prenom + " " + nom
    end

    def habite_en(valeur)
       valeur == pays
    end
end

bob = Utilisateur.new("Bob")
bob.nom = "Lewis"
bob.pays = "France"

puts bob.prenom + " " + bob.nom
bob.nom_complet
puts bob.habite_en("France")
```

Run:
```
> ruby file.rb
Bob Lewis
Bob Lewis
true
```

### Return

In a function or a method:
```
return <value>
```

## Methods

### Common

#### class

Get class name:
```
> 10.class
=> Integer
> 78.5.class
=> Float
> true.class
=> TrueClass
```
