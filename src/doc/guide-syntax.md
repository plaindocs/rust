% The Guide to Rust Syntax

A *very* brief guide to Rust syntax. It assumes you are already familiar with programming concepts. 

# Assert macro

The `assert!` macro ends the program if the condition passed to it is not true:

~~~
fn main() {
  assert!(4==5);
  println("This is never printed.");
}
~~~

Normally used in [testing][testing] blocks.

[testing]: http://doc.rust-lang.org/master/guide-testing.html

# Conditional Statements

Conditions structures use the `if` keyword, and can have optional `else` structures which can be chained together. The condition must be of type `bool` (there is no implicit conversion), and is not wrapped in parentheses.

~~~
if false {
    println!("that's odd");
} else if true {
    println!("right");
} else {
    println!("neither true nor false");
}
~~~

If the `if`/`else`/`else if` arms are blocks that have a value, this value must be of the same type for every arm in which control reaches the end of the block:

~~~
fn signum(x: int) -> int {
    if x < 0 { -1 }
    else if x > 0 { 1 }
    else { 0 }
}
~~~

Read the Rust reference to [If expressions][if].

[if]: http://doc.rust-lang.org/master/rust.html#if-expressions

# Enumerations

Enumerations are datatypes with several alternate representations. A simple `enum`
defines one or more constants, all of which have the same type:

~~~~
enum Direction {
    North,
    East,
    South,
    West
}
~~~~

Each variant of this enum has a unique and constant integral discriminator value. If no explicit discriminator is specified for a variant, the value defaults to the value of the previous variant plus one. If the first variant does not have a discriminator, it defaults to 0. For example, the value of North is 0, East is 1, South is 2, and West is 3.

When an enum has simple integer discriminators, you can apply the as cast operator to convert a variant to its discriminator value as an int:

~~~
println!( "{:?} => {}", North, North as int );
~~~

It is possible to set the discriminator values to chosen constant values:

~~~
enum Color {
  Red = 0xff0000,
  Green = 0x00ff00,
  Blue = 0x0000ff
}
~~~

The Rust reference to [enumerations][enum].

[enum]: http://doc.rust-lang.org/master/rust.html#enumerations

# Functions

Functions in Rust are introduced with the `fn` keyword, optional arguments are specified within parenthesis as comma separated `name: type` pairs, and `->` indicates the return type. You can ommit the return type for functions that do not return a value. Functions return the top level expression (note the return expression is not terminated with a semi colon).

~~~~
fn increment(i:int) -> (int) {
    // Returns i+1
    i + 1
}

fn main() {
    let i = 7;

    let k = increment(i); // k=8
}
~~~~

The Rust reference to [functions][functions].

[functions]: http://doc.rust-lang.org/master/rust.html#functions

# Loops

Looping over code is familiar to every programmer, in Rust this is achieved with the `loop` and `while` structures, the bodies of loop structures must be wrapped in braces, and the control condition of the `while` and `for` loops does not need to be wrapped in parentheses.

`break` exits from loops, and `continue` exits the current iteration and continues with the next. 

The simplest type is `loop`, which loops forever until a `break` exits the loop. 

~~~
fn main() {
    /* A simple loop */
    loop {
        //Loops until a break
        break;
        }
    }
}
~~~

More information on [while loops][loops] and [for loops][for].

[loops]: http://doc.rust-lang.org/master/rust.html#while-loops
[for]: http://doc.rust-lang.org/master/rust.html#for-expressions

## For loops

`for` loops iterate over a range of numbers.

~~~
for n in range(0, 5) {
    println!("{}", n);
}
~~~

## While loops

`while` loops until a condition is met.

~~~
let mut count = 0;

while count < 10 {
    println!("count is {}", count);
    count += 1;
}
~~~

# Macros

Macros are extensions to the core Rust syntax provided by libraries, and are introduced by an indentifier followed by an exclamation mark, as shown by `println!` in the following hello world example:

~~~
fn main() {
    println!("hello?");
}
~~~

Read the guide to [writing macros][guide-macro] for more information.

[guide-macro]: http://doc.rust-lang.org/0.10/guide-macros.html

# Operators

Rust's set of operators contains very few surprises. Arithmetic is done with
`*`, `/`, `%`, `+`, and `-` (multiply, quotient, remainder, add, and subtract). `-` is
also a unary prefix operator that negates numbers.kelAs in C, the bitwise operators
`>>`, `<<`, `&`, `|`, and `^` are also supported.

Note that, if applied to an integer value, `!` flips all the bits (bitwise
NOT, like `~` in C).

The comparison operators are the traditional `==`, `!=`, `<`, `>`,
`<=`, and `>=`. Short-circuiting (lazy) boolean operators are written
`&&` (and) and `||` (or).

The Rust reference to [binary operators][binary].

[binary]: http://doc.rust-lang.org/master/rust.html#binary-operator-expressions

# Primitive types

Rust has the following primive types:

* Signed integer: `int`, `i8`, `i16`, `i32`, `i64`. Specify hexadecimal, octal or binary notation by prefixing with `0x`, `0o` or `0b`.
* Unsigned integer: `uint`, `u8`, `u16`, `32`, `i64`.
* Floating point: `f32` and `f64`.
* `char`
* `bool`: either `true` or `false`.

~~~
let a = 1;       // `a` is an `int`
let b = 10i;     // `b` is an `int`, due to the `i` suffix
let c = 100u;    // `c` is a `uint`
let d = 1000i32; // `d` is an `i32`
~~~

More information on [strings and literals][strings].

[strings]: http://doc.rust-lang.org/master/rust.html#literals

# Print macro

The `print!` and `println!` macros are the Rust equivalent of C's `printf`. They take a string with placeholders (`{}`) and variables or strings. `println!` adds a new line to the end of the output. 

~~~
var w="world";
println("Hello {}", w); 

// {} will print the "default format" of a type
println!("{} is {}", "the answer", 43);

// {:?} will conveniently print any type
println!("what is this thing: {:?}", mystery_object);
~~~

Read more information on [formating and printing][fmt].

[fmt]: http://doc.rust-lang.org/0.10/std/fmt/

# Structs 

Structs are collections of data types, and use a syntax similar to structs in C `struct Name { field1: type1, field2: type2, field3: type3 [, ...] } `

~~~
struct Point {
    x: f64,
    y: f64
}

let mypoint = Point {x: 1.0, y: 2.0};

//Access individual fields using the dot operator.
println! (mypoint.x); 
~~~

All fields of a struct are mutable if the struct itself is mutable. 

The Rust reference to [structs][structs].

[structs]: http://doc.rust-lang.org/master/rust.html#structures

# Testing

To test your Rust code without increasing the size of the compiled program, use the `#[test]` attribute.

~~~
fn main() {
    println!("hello?");
}

#[test]
fn testing_something() {
  assert(4==5);
}
~~~

Run tests using `rustc --test foo.rs` and compile your program without the test code using `rustc foo.rs`. More information on [testing][testing].

# Tuples

Tuples in Rust behave exactly like structs, except that their fields do not
have names. Thus, you cannot access their fields with dot notation.  Tuples
can have any arity (number of elements) except for 0 (though you may consider
unit, `()`, as the empty tuple if you like).

~~~~
let mytup: (int, int, f64) = (10, 20, 30.0);
match mytup {
  (a, b, c) => info!("{}", a + b + (c as int))
}
~~~~

The Rust reference to [structs][structs].

[structs]: http://doc.rust-lang.org/master/rust.html#structures

# Variables

There are two types of variable in Rust:

* `immutable` - the value cannot be changed. Introduced with `let`.
* `mutable` - the value of can be changed. Introduced with `let mut`.

~~~
fn main() {

    let i = 7; // i Cannot be changed 

    let mut j = i +1; // j = 8
    
    j = 9; // j can be changed

}
~~~
