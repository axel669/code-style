# Axel's Javascript Style Guide v1.0.0

> "Perfection is achieved, not when there is nothing left to add, but when
> there is nothing left to take away"
>
> _- Antoine de Saint-Exupéry_

> "I have yet to see any problem, however complicated, which, when you looked at
it in the right way, did not become still more complicated."
>
> _- Anderson's Law (Poul Anderson)_

> The simplest way to fix an error is to not make it in the first place.

<!-- TOC -->

- [Axel's Javascript Style Guide v1.0.0](#axels-javascript-style-guide-v100)
    - [Formatting](#formatting)
        - [Semicolons](#semicolons)
        - [Curly Braces](#curly-braces)
        - [Flow Control](#flow-control)
        - [Indentation](#indentation)
        - [Line Length](#line-length)
        - [Statements](#statements)
        - [Line Wrapping](#line-wrapping)
        - [Blank Lines](#blank-lines)
        - [Parentheses](#parentheses)
        - [Comments](#comments)
    - [Naming](#naming)
        - [Base Rules](#base-rules)
        - [Variables](#variables)
        - [Functions](#functions)
    - [Language Features](#language-features)
        - [Variable Declarations](#variable-declarations)
        - [Strings](#strings)
            - [Construction](#construction)
            - [Concatenation](#concatenation)
            - [Multiline](#multiline)
        - [Numbers](#numbers)
        - [Arrays](#arrays)
            - [Construction](#construction)
            - [Non-numeric Properties](#non-numeric-properties)
            - [Destructuring](#destructuring)
        - [Objects](#objects)
            - [Construction](#construction)
            - [Numeric Properties](#numeric-properties)
            - [Property Shorthand](#property-shorthand)
            - [Destructuring](#destructuring)
            - [Enums](#enums)
        - [Functions](#functions)
            - [Functions as arguments](#functions-as-arguments)
        - [Flow Control](#flow-control)
            - [`if`](#if)
            - [`try`/`catch`](#trycatch)
            - [`while` Loops](#while-loops)
            - [`for` Loops](#for-loops)
        - [Disallowed Features](#disallowed-features)
            - [`else`](#else)
            - [`switch`](#switch)
            - [`class`](#class)
            - [`this`](#this)
            - [`with`](#with)
            - [`eval`](#eval)
            - [No long functions](#no-long-functions)

<!-- /TOC -->

## Formatting

### Semicolons
Don't use them. Following this guide will ensure that JS's Automatic Semicolon
Insertion (ASI) will never get it wrong.

### Curly Braces
Always use curly braces on flow control structures, even when optional.

Curly braces should always go on the same line as the start of the information
it wraps. We aren't barbarians here.

```javascript
//  Correct
if (a === 1) {
    thing()
    otherThing()
}
```

```javascript
//  Correct
while (a < 10) {
    doStuff()
}
```

```javascript
//  Correct
for (const item of collection) {
    doStuff()
}
```

### Flow Control
Flow control keywords should always begin a line.

```javascript
if (a === 0) {
}

try {
}
catch (err) {
}
```

### Indentation
Fun fact: there has only been a single study ever conducted on the effects of
indentation on code readability. It has a number of glaring errors, so there's
currently 0 proof of any functional advantage of what the "correct" amount is.

Use 4 spaces for indentation. The tab key is for the typewriter, and we don't
have that kind of backwards compatibility.

### Line Length
Limit to 80 characters max on a single line. Not everyone has an IMAX screen
as a monitor, and we don't have a theater to project onto for code reviews.
If you need to get a waterskin and backpack to find the end of the line,
rethink what you're doing.

Fun fact: humans read best at 60 character columns, so 80 is pretty generous.

**Note:** The column limit in conjunction with 4 space indentation can provide
hints as to when too much nesting is being done in one area.

### Statements
A single line should have no more than 1 statement.

```javascript
//  Do this
thing1()
thing2()

//  Don't do this. ever.
thing1() thing2()
```

### Line Wrapping
These are the rules for wrapping lines to keep them within the 80 character
limit

When breaking expressions into multiple lines, indent every line that does work
after the first
- Never wrap array access or expressions within array access
- When breaking lines on operators, the operator should begin the next line and
    the closing paren should be on its own line at the same indentation level
    as the call
- Property access should always include the `.` on the new line
- When breaking function calls, every argument gets at least one line
- When breaking React components into multiple lines all properties get their
    own lines and are indented, and the end of the tag goes on its own line
    at the same indentation level as the tag opening
- Commas end lines, they don't begin them. I'm looking at you C# `>:|`
- Recursively apply these rules as necessary

### Blank Lines
Use blank lines to separate parts of code with distinct purposes within a
function.

Do not put a blank line as the first line of a function; It's ugly and if the
start of your function is logically separate from the name of the function,
rethink your naming.

### Parentheses
- Flow controls have a space between keywords and parens
- Function calls have no space between the function name and the parens
- Wrap mathematical expressions in parens if they span more than one line
    and are outside of a function argument list
- **Always** group similar logical operations with parens
- Always group bitwise operations with parens

```javascript
//  Do this
if (expression) {}
while (expression) {}
switch (expression) {}
for (const item of collection) {}

Math.sin(pi)
console.log(stuff)
fetch(url)

const value = (
    (someValue + otherValue + anotherValue - adjustmentValue)
    / wat
)
showNumber(
    (someValue + otherValue + anotherValue - adjustmentValue)
    / wat,
    secondArg
)

if ((a && b) || c) {}
if (a || b || (c && d && e)) {}

const why = (index ^ mask) + 1
```

### Comments
Don't write comments in your code.

> "A common fallacy is to assume authors of incomprehensible code will somehow
    be able to express themselves lucidly and clearly in comments."
>
> _- Kevlin Henney_

> "Comments are a delicate matter, requiring taste and judgement. I tend to err
    on the side of eliminating comments, for several reasons. First, if the code
    is clear, and uses good type names and variable names, it should explain
    itself. Second, comments aren't checked by the compiler, so there is no
    guarantee they're right, especially after the code is modified. A misleading
    comment can be very confusing. Third, the issue of typography: comments
    clutter code."
>
> _- Rob Pike, "Notes on Programming in C"_


## Naming
Always use meaningful names given the context of the function. Our programs
don't exist in voids, use that contextual information to communicate your
code's intention more effectively.

### Base Rules
- Use camel casing
- Don't use underscores in names. Underscores in JS are historically used for
    "private" variables and functions, but with closures that is no longer a
    concern for code.

### Variables
- Use `is<X>` for toggles
- Use `should<X>` for future decision variables
- Use `prev<X>`, `current<X>`, and `next<X>` when dealing with history

### Functions
- Don't use `is<X>`, the language has all of the `is` checks you should need
- Use `should<X>` to determine future actions
- Use `<verb>Prev<X>`, `<verb>Current<X>`, and `<verb>Next<X>` when dealing with
    history

## Language Features

### Variable Declarations
- Only use `let` and `const`
- Make all variables `const` by default. Only make something mutable if it MUST
    change
- Only declare one variable per line. None of this comma separated variables
    nonsense
- Declare variables when they are needed isntead of grouping everything at the
    top of the scope they are used in.
    - _Logical Scope !== Lexical Scope_

### Strings

#### Construction
- Never use the `String` constructor
- Use double quotes (`"`) or backticks (`` ` ``) only.

#### Concatenation
- Concatenation should be done with template literals `` `${head}${tail}` ``
- For large groups of strings, use array joins to concat

#### Multiline
- All multiline strings should use template literals
- Long strings that should not be multiline should use the array join style

```javascript
//  Array-join
const longString = [
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod",
    "tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim",
    "veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea",
    "commodo consequat. Duis aute irure dolor in reprehenderit in voluptate",
    "velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint",
    "occaecat cupidatat non proident, sunt in culpa qui officia deserunt",
    "mollit anim id est laborum.",
].join(" ")
```

### Numbers
Decimal,

All of the numeric styles are good, just be sure to apply them where it makes
sense. Because we have access to binary (`0b`), octal (`0o`), and hex (`0x`),
omit all leading zeroes on decimal numbers.
- Never use the `Number` constructor

### Arrays

#### Construction
- Never use the `Array` constructor
- Use the spread operator to concat arrays by making a new one
- Use trailing commas, it makes adding and reordering elements much easier

```javascript
const a1 = [1, 2,]
const a2 = [3, 4,]

const concatenated = [...a, ...b,]
```

#### Non-numeric Properties
Don't add non-numeric properties to an array

#### Destructuring
- Omit trailing commas, this is not creating arrays, it's pulling them apart
- Destructuring allows arrays to be used in place of tuples, and this behavior
    is encouraged
- Always put default values at the element level

```javascript
//  Cheap swap trick \o/
[a, b] = [b, a]

const [first = 0, second = 1] = rangeTuple

const func = ([head = 0, ...tail]) => head + tail.length
```

### Objects

#### Construction
- Never use the `Object` constructor
- Use trailing commas, it makes adding and reordering properties much easier
- Don't use the method shorthand, always use arrow functions. If `this` appears,
    you've done something wrong
- String keys should use double quotes, they are strings after all
- Computed property names are your friend too
- Use the spread operator to merge objects

```javascript
const example = {
    ...baseObject,
    prop: "value",
    theAnswer: 42,
    "not-a-value": null,
    [`${keyPart1}-${keyPart2}`]: "wat",
    func: () => {
        doStuff()
        return things
    },
}
```

#### Numeric Properties
Don't add numeric properties to objects, what you want is the `Map`

#### Property Shorthand
Use the property shorthand syntax whenever possible

```javascript
const angle = 1.2 * Math.PI
const magnitude = 4.2
const polarPosition = {angle, magnitude}
```

#### Destructuring
- Use trailing commas if the statement spans multiple lines
- Always put default values at the element level
- Avoid destructuring more than one level at a time
- Do not attempt to destructure computed properties
- When destructuring 4+ item, put each destructured variable on its own line,
    with the assignment as the last line

```javascript
function Component(props) {
    const {position, style} = props
    const {angle, magnitude} = position
}

const {
    angle,
    magnitude,
    viscosity,
    luminosity,
} = options
```

#### Enums
Enum names and properties should be pascal cased. Do not use property names
that require array access to use or computed properties, and do not
destructure enums.

```javascript
const GoodEnum = {
    FirstValue: 10,
    SecondValue: 100,
}
```

```javascript
//  Don't do any of this
const badEnum = {
    [`Computed-${propName}`]: "bad",
    "bad-name": null,
    anotherBadName: "wat",
}
function Stuff(value) {
    const {FirstValue} = GoodEnum
}
```

### Functions
- Always use arrow functions to create data processing functions, even on
    objects literals
- Use closures instead of binding
- Capitalize cosntructor-style functions (functions that create objects with
    interfaces as opposed to simply transforming data)
- Don't have more than 3 items in an argument list unless the context of the
     function makes the order of the argument obvious (hint: it never will)
    - Variadic arguments count as one item
    - Use objects and destrucuring when a large amount of information is needed
        for a call
    - Destructure arguments in the function body

```javascript
//  Data processing
const square = n => n ** 2
const formatInit = (info) => {
    const {value, mod} = info
    const plus = "+".repeat(
        Math.max(0, mod)
    )
    const minus = "-".repeat(
        Math.max(0, -mod)
    )

    return `${value}${plus}${minus}`
}
```

```javascript
//  Constructor-style
const addition = (left, right) => left + right
const BinaryOp = (left, right, op) => {
    return {
        left,
        right,
        calc: () => op(left, right),
    }
}
const addOp = BinaryOp(1, 2, addition)
```

```javascript
//  In object literals
const number = {
    isEven: n => (n % 2) === 0,
    absoluteValue: n => {
        if (n < 0) {
            return -n
        }
        return n
    }
}
```

```javascript
//  Variadic args
//  1 item
const compose = (...funcs) => {
    doStuff(funcs)
}
//  2 items
const fetchPOST = (url, options) => {
    const {
        data,
        type,
        timeout = 10,
        cors = true
    } = options
    doStuff()
}
```

#### Functions as arguments
When a function call or function declaration is an argument to another function
call, always split the arguments as per the rules in the Line Wrapping section
(each arguments gets a line, apply recusively).

### Flow Control

#### `if`
Only use guard-clause style if statements. Do not allow code to flow through `if`s,
only around.

#### `try`/`catch`
Use try-catch blocks when exceptions can occur in the code that needs to be
handled by the function. Always name the error variable `err`. Empty catch
statements are allowed.

#### `while` Loops
A `while` loop's condition should never take up more than one line. If the
condition needs to make a number of checks, use closures to move the checks
into a function call instead.

Do not use the `do-while` loop, use `while (true)` with a `break`.

```javascript
//  Simple loop
while (a < b) {
}
```

```javascript
//  Complex loop conditions
const values = [1, 2, 3, 4]
const sum = arr => arr.reduce((a, b) => a + b, 0)
const check = () => (
    values[0] < values[1]
    && values[1] <= values[2]
    && values[2] < values[3]
    && (sum(values) % 3) === 1
)
while (check()) {
}
```

```javascript
//  do-while syntax is bad
while (true) {
    doStuff()

    if (condition) {
        break
    }
}
```

#### `for` Loops
Only use the `for-of` loop, and always make the iteration value `const`. To
iterate over objects use `for-of` over the result of `Object.keys`,
`Object.values`, or `Object.entries`. Destructuring in iteration items is
encouraged.

```javascript
//  Destructure iterator
for (const item of collection) {
}
for (const [head, ...tail] of lists) {
}
for (const {name, value} of nodes) {
}
```

```javascript
//  Iterate through object information
for (const key of Object.keys(obj)) {
}

for (const value of Object.values(obj)) {
}

for (const [key, values] of Object.entries(obj)) {
}
```

### Disallowed Features
All of the features here should never be used unless a library mandates their
usage. If that is the case, reconsider the usage of that library.

#### `else`
Don't use the `else` keyword at all. use of the `?:` is still allowed but as
always should be restricted to short values. This also means if-else chains
should never exist in code.

#### `switch`
Don't use the switch keyword. well constructed functions and tables do the work
without any of the weird rules.

#### `class`
JavaScript doesn't need classes, and JS classes don't actually use classical
inheritance. This keyword is the greatest mistake in the language to date.

#### `this`
Don't use the `this` keyword. Closures will net the same benefits without any
of the issues.

#### `with`
The `with` keyword does weird things to the scope of executing code. It
requires a table just to keep its rules straight, avoid at all cost.

#### `eval`
`eval` is almost exclusively used in the wrong way and has very few restrictions
in what it allows arbitrary code to do, avoid it. Using the `Function`
constructor is recommended when dynamic code execution cannot be avoided
because it has the same limitations as a function.

#### No long functions
Limit all functions to no more than 30 LOC. Bonus points if the LOC all fit in
30 lines of text.
