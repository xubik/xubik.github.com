---
layout: post
tagline: Notes from the only guide to Ruby
---
{% include JB/setup %}

Reference: <http://mislav.uniqpath.com/poignant-guide/>

## Chapter 2 Kon’nichi wa, Ruby

>This book is a poignant guide to Ruby. That means code so beautiful that tears are shed.

Three reasons to learn Ruby:

1. Brain Health
>Creative skills, people. Deduction. Reason. Nodding intelligently. The language will become a tool for you to better connect your mind to the world. I’ve noticed that many experienced users of Ruby seem to be clear thinkers and objective. (In contrast to: heavily biased and coarse.)
2. One man on an island
>Ruby was born in Japan. Which is freaky. Japan is not known for its software. And since programming languages are largely written in English, who would suspect a language to come from Japan?
>It’s triumphant and noble and all that. Support diversity. Help us tilt the earth just a bit.
3. Free
>Using Ruby costs nothing. The code to Ruby itself is open for all of the world to inhale/exhale. Heck, this book is free. It’s all part of a great, big giveaway that should have some big hitch to it.

>With that, it’s time for the book to begin. You can now get out your highlighter and start dragging it along each captivating word from this sentence on. I think I have enough hairspray and funny money on my person to keep me sustained until the final page.

## Chapter 3 A Quick (and Hopefully Painless) Ride Through Ruby (with Cartoon Foxes)

### The parts of speech

Part | Notes | Examples 
---|---|---
Variables | Plain, lowercase words consisting of letters, digits and underscores | `x`, `y`, `banana2`, `phone_a_quail`
Numbers | Integers or floats, plus or minus, floats have decimal places and can be written in scentific notation | `2`, `-10000`, `3.14`, `12.043e-04`
Strings | Any sort of characters surrounded by quotes | `"sealab"`, `'2021'`, `"These cartoons are hilarious!"`
Symbols | Words looking like variables, starting with a colon, lightweight strings usually used when you won't be printing the string to the screen | `:a`, `:b`, `:ponce_de_leon`
Constants | Like variables but capitalised | `Time`, `Array`, `Bunny_Lake_is_Missing`
Methods | Verbs, usually attached to the end of variables by a dot, both exclamation marks and question marks can be used in method names | `open`, `close`, `is_open?`
Method arguments | Arguments are attached to the end of a method surrounded by parentheses and separated by a comma | `front_door.paint( 3, :red )`
Kernel methods | Common methods, don't usually use parentheses | `print "See, no dot."`
Class methods | Usually attached after variables and constants, joined by a double colon | `Door::new( :oak )`
Global variables | Variables beginning with `$` | `$x`, `$1`, `$chunky`, `$CHunKY_bACOn` 
Instance variables | Variables beginnin with `@`, often used to define the attributes of something | `@width`
Class variables | Variables beginning with `@@`, defines an attribute for every object in a class | `@@x`, `@@y`, `@@i_will_take_you`
Blocks | Any code surrounded by curly braces or `do` and `end` | `2.times { print "yes, never again" }`
Block arguments | A set of variables surrounded by pipe characters, used at the beginning of a block | 
Ranges | Two values surrounded by parentheses and separated by an ellipsis, a third dot indicates that the final value is not included | `(1..3)`, `('a'..'z')`, `(0...5)`
Arrays | A list surrounded by square brackets, a collection of things, but kept in a specific order | `[1, 2, 3]`, `['coat', 'mittens', 'snowboard']`
Hashes | A dictionary surrounded by curly braces, matches words to definitions | `{'a' => 'aardvark', 'b' => 'badger'}`
Regular expressions | Regex surrounded by slashes | `/ruby/`, `/[0-9]+/`, `/^\d{3}-\d{3}-\d{4}/`
Operators | Required for maths or comparing things | !  ~  *  /  %  +  -  &
Keywords | Ruby has a number of built-in words, imbued with meaning | return self super

## Chapter 4 Floating Little Leaves of Code

### Animal perfect mission statement




