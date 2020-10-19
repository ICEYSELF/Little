# Little
Little is a dynamic strong typed script Programming Language


## Example

```little

// Module Declaration
module Hello;        // Module name must be same with current file name.

// Import Declaration
import Prelude;     // Search current directory firstly, search custom directory secondly;
import MyModule;

// Bindings
// multiExpression = <expression>; | '{' (<expression>;)+ [expression] '}'
// binding ::= [export] <partten> = multiExpression
// bindings is avaliable on current context only.
// if current context is already has this name, compiling will fail.

// Basic Types
null = ();   // null
b1 = true;   // bool
b2 = false;  // bool
num1 = 1;    // i32 (int32)
num2 = 1i32; // i32 (int32)
num3 = 1u;   // u32 (uint32)
num4 = 1u32; // u32 (uint32)
num5 = 1i8;  // i8 (int8)
num6 = 1u8;  // u8 (uint8)
num7 = 1i16; // i16 (int16)
num8 = 1u16; // u16 (uint16)
num9 = 1i64; // i64 (int64)
num10 = 1u64; // u64 (uint64)
num11 = 1.0f;   // f32 (float32)
num12 = 1.0f32; // f32 (float32)
num13 = 1.0;    // f64 (float64)
num14 = 1.0f64; // f64 (float64)
num15 = 100big; // big (Big Integer)
export num16 = 100.0fbig; // fbig (Big Float) and you can get this value by outside.

// Functions
// function ::= <partten>+ -> multiExpression
// apply ::= <functionExpression>'('<parameterExpression>')'
f1 = (a, b) -> a + b;
f2 = a -> a + 1;
f3 = (a, b) -> {
    sum = a + b;
    sum
};
apply = f1(1, 2);

// Partten Matching
matchingFunction = function {
    (a, b) -> a + b;
    a -> a + 1;
    |EmptyList| -> empty;
    |List| (head, |EmptyList|) -> list with 1 element;
    |List| (head, tail)-> list with elements;
};

// Mutable Values
// mutable is a function, it will create a reference cell to wrap the value.
// you can call "set" function in mutable reference cell.
mutableValue = mutable 1i32;    // mutable is a function in global context.
mutableValue.set 2i32;    // reset value
mutable.value;    // get the value

// String and List
str = "abcdef";    // 'list i8' type, UTF-8
str2 = "abcdef"utf8;  // 'list i8' type, UTF-8
str3 = "abcdef"utf16; // 'list i16' type, UTF-16
str4 = "abcdef"utf32; // 'list i32' type, UTF-32
str5 = @"abcdef\";    // original string
str6 = """
super string!!!
""";                  // multiline string

ls = list { 1; 2; 3; 4; 5; 6 };    // List Monad
lsLazy = seq { 1; 2; 3; 4; 5; 6 }; // Sequence Monad (Lazy List)
lsFirst = ls.get(0);
lsSecond = ls.get(1);
lsSlice = ls.slice(0, 3);  // list { 1; 2; 3; 4 }

// Tuple
tuple = (1, 2);
(first, second) = tuple;

// Print
// printf : formatString -> formatAndPrintFunction
// sprintf : formatString -> formatAndSprintFunction

// Records
a = {
    a = "abc";
    b = "abcd";
    export addWithA = x -> x + a;
};

b = a with { b = "this is a b!"; c = "c"; export addWithA = fn x -> x + a; };

// Tagged Union
valueA = |ParttenA|             // Matches |ParttenA|
valueB = |ParttenB|             // Matches |ParttenB|
valueC = |Partten| 1;           // Matches |Partten| 1 or |Partten| x or |Partten| _ or _
valueD = |Partten| (1, 2);      // Matches |Partten| (1, 2) or |Partten| (x, y) or |Partten| x or |Partten| _ or _

// Active Partten
|SomePartten| (x, y) = function {
    x, y -> |SomePartten| (x, y);  // Make (x, y) Matches |SomePartten| (1, 2)
    _ -> ()                        // Not Matches
};

// Monad
option = {
    return = a -> |Some| a;
    unit = |None|;
    bind = (f, a) ->
      function {
          |Some| x -> |Some| (f x);
          |None| -> |None|;
      }(a);
    // combine
    // combineUnwrap
    // for
    // while
    // do
};

opt1 = option {
    bind x = return 1 + 2;
    return x + 1
};

resultMonad = try {
    bind x = download "baidu.com";
    return x
};

// if expression
ifResult = if a > 1 { 1 } else { 2 };

if a > 1 {
    something;
};

// loop expression
loop {
    something;
};

// while expression
while true {
    something;
    break;
    continue;
};

// for expresion
for i in something {
    something;
    break;
    continue;
};
```
