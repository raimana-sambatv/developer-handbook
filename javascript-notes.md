# JavaScript Notes
- [JavaScript Notes](#javascript-notes)
  - [Types](#types)
    - [List each type, if it's a primitive or built-in type, its `typeof` return values, and its distinct value(s).](#list-each-type-if-its-a-primitive-or-built-in-type-its-typeof-return-values-and-its-distinct-values)
    - [Are types attached to variables or values?](#are-types-attached-to-variables-or-values)
    - [Which types are immutable and which types are mutable?](#which-types-are-immutable-and-which-types-are-mutable)
    - [What is the difference between a variable whose value is `undefined` or `null`? How can they be checked?](#what-is-the-difference-between-a-variable-whose-value-is-undefined-or-null-how-can-they-be-checked)
    - [What is `NaN` and when does it occur? How can it be checked?](#what-is-nan-and-when-does-it-occur-how-can-it-be-checked)
    - [Why is there `-0`, how can it be checked, and how can it be useful?](#why-is-there--0-how-can-it-be-checked-and-how-can-it-be-useful)
    - [What is boxing?](#what-is-boxing)
    - [Why is there a bias against implicitness and what's a better way to think about it?](#why-is-there-a-bias-against-implicitness-and-whats-a-better-way-to-think-about-it)
    - [How are the abstract and strict equality operators alike and different?](#how-are-the-abstract-and-strict-equality-operators-alike-and-different)
    - [In summary, what is the best way to work with JavaScript's type system?](#in-summary-what-is-the-best-way-to-work-with-javascripts-type-system)
  - [Scope](#scope)
    - [Why is scope important?](#why-is-scope-important)
    - [What is scope?](#what-is-scope)
    - [What type of scope does JavaScript use and when is it determined?](#what-type-of-scope-does-javascript-use-and-when-is-it-determined)
    - [What is the difference between an undefined and undeclared variable?](#what-is-the-difference-between-an-undefined-and-undeclared-variable)
    - [When are global variables automatically created?](#when-are-global-variables-automatically-created)
    - [What is strict mode and when should it be used?](#what-is-strict-mode-and-when-should-it-be-used)
    - [In terms of grammar, what is the difference between a function declaration and a function expression?](#in-terms-of-grammar-what-is-the-difference-between-a-function-declaration-and-a-function-expression)
    - [In terms of scope, what is the difference between a function declaration and a function expression?](#in-terms-of-scope-what-is-the-difference-between-a-function-declaration-and-a-function-expression)
    - [What are three reasons to use named function expressions over anonymous function expressions?](#what-are-three-reasons-to-use-named-function-expressions-over-anonymous-function-expressions)
    - [As a general rule of thumb, what is the heirarchy of best ways to create a function?](#as-a-general-rule-of-thumb-what-is-the-heirarchy-of-best-ways-to-create-a-function)
    - [What is the difference between lexical scope and dynamic scope?](#what-is-the-difference-between-lexical-scope-and-dynamic-scope)
    - [What is the principle of least privilege and why is it useful?](#what-is-the-principle-of-least-privilege-and-why-is-it-useful)
    - [What is an IIFE and why is it useful?](#what-is-an-iife-and-why-is-it-useful)
    - [What is hoisting?](#what-is-hoisting)
    - [What is the temporal dead zone?](#what-is-the-temporal-dead-zone)
    - [What is a closure?](#what-is-a-closure)
    - [What is a module?](#what-is-a-module)
  - [Objects](#objects)
  - [ECMAScript Specification](#ecmascript-specification)
    - [What are the three main parts of the ECMAScript specification?](#what-are-the-three-main-parts-of-the-ecmascript-specification)
    - [Abstract Operations](#abstract-operations)
      - [How does `ToPrimitive(input [, PreferredType])` coerce objects to primitives?](#how-does-toprimitiveinput--preferredtype-coerce-objects-to-primitives)
      - [What are the `ToString(argument)` return values for each type?](#what-are-the-tostringargument-return-values-for-each-type)
      - [What are the `ToNumber(argument)` return values for each type?](#what-are-the-tonumberargument-return-values-for-each-type)
      - [What are the `ToBoolean(argument)` return values for each type?](#what-are-the-tobooleanargument-return-values-for-each-type)
  - [Learning Resources](#learning-resources)

---

## Types

### List each type, if it's a primitive or built-in type, its `typeof` return values, and its distinct value(s).
| Type     |Primitive or Built-In |`typeof` Return Values     |Distinct Values                             |
|----------|----------------------|---------------------------|--------------------------------------------|
|String    |Primitive             |`'string'`                 |                                            |
|Number    |Primitive             |`'number'`                 |`0`, `-0`, `Infinity`, `-Infinity`, `NaN`   |
|Boolean   |Primitive             |`'boolean'`                |`true` or `false`                           |
|Undefined |Primitive             |`'undefined'`              |`undefined`                                 |
|Null      |Primitive             |`'object'`                 |`null`                                      |
|Symbol    |Primitive             |`'symbol'`                 |                                            |
|Object    |Built-In              |`'object'` or `'function'` |                                            |

References
- https://tc39.github.io/ecma262/#sec-ecmascript-language-types
- https://tc39.github.io/ecma262/#sec-typeof-operator

**[[ ↑ ] Back to top](#javascript-notes)**

---

### Are types attached to variables or values?
Values have types, not variables.

References
- https://frontendmasters.com/courses/deep-javascript-v3/primitive-types/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### Which types are immutable and which types are mutable?
All primitive types are immutable and the built-in Object type is mutable.

References
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Primitive_values

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is the difference between a variable whose value is `undefined` or `null`? How can they be checked?
When a variable is declared with `var` or `let` and not assigned a value, it is initialized with the value `undefined`.

Both `undefined` and `null` can be checked with the equality operators.

References
- https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md#whats-the-difference-between-a-variable-that-is-null-undefined-or-undeclared-how-would-you-go-about-checking-for-any-of-these-states

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is `NaN` and when does it occur? How can it be checked?
`NaN` represents an invalid number during invalid numerical operations, like trying to coerce an incompatible value to a number.

`NaN` is the only value that is not equal to itself so the inequality operators can check for it. There's the more semantic `isNaN` function but it can return unexpected results due to coercing its argument to a number. So the preferred method is `Number.isNaN()`, which checks for `NaN` without coercion.

References
- https://frontendmasters.com/courses/deep-javascript-v3/nan-isnan/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### Why is there `-0`, how can it be checked, and how can it be useful?
JavaScript uses the IEEE 754 standard that requires all numbers to be signed.

None of the comparison operators can distinguish `-0`, so use `Object.is()` or try dividing a number by it to check for it.

A signed zero can provide additional information about how something was last changing before it stopped changing, like a stock trend or position of a car.

References
- http://2ality.com/2012/03/signedzero.html
- https://frontendmasters.com/courses/deep-javascript-v3/negative-zero/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is boxing?
'Boxing' refers to the implicit coercion of primitives into objects when trying to access their properties and methods.

References
- https://frontendmasters.com/courses/deep-javascript-v3/boxing/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### Why is there a bias against implicitness and what's a better way to think about it?
Implicit mechanisms are associated with being bad because they do things behind the scenes. Implicitness is better thought of as abstraction. While it isn't always good, it can be necessary because it hides unneccesary details and allows the reader to focus on what's important.

References
- https://frontendmasters.com/courses/deep-javascript-v3/implicit-coercion/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### How are the abstract and strict equality operators alike and different?
If the types are the same, they do the same thing. If not, the abstract equality operator performs coercion. Specifically if the types are `null` and `undefined`, it will return `true` or try to generally convert each type into a number.

References
- https://tc39.github.io/ecma262/#sec-abstract-equality-comparison
- https://frontendmasters.com/courses/deep-javascript-v3/double-equals-summary/
- https://dorey.github.io/JavaScript-Equality-Table/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### In summary, what is the best way to work with JavaScript's type system?
The most important thing to do is to always understand the types used and make them obvious.

References
- https://frontendmasters.com/courses/deep-javascript-v3/understanding-your-types/

**[[ ↑ ] Back to top](#javascript-notes)**

---

## Scope

### Why is scope important?
It improves code organization, including but not limited to closures and the module pattern.

References
- https://frontendmasters.com/courses/deep-javascript-v3/scope/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is scope?
The extent where identifiers are available, whether it's global, in functions, or in scopes.

References
- https://frontendmasters.com/courses/deep-javascript-v3/scope/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What type of scope does JavaScript use and when is it determined?
Lexical scope and it is determined before runtime.

References
- https://frontendmasters.com/courses/deep-javascript-v3/lexical-scope-review/
- https://frontendmasters.com/courses/deep-javascript-v3/lexical-dynamic-scope/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is the difference between an undefined and undeclared variable?
An undefined variable is one that has been declared and has the value `undefined`. An undeclared variable doesn't exist and doesn't hold any value because it was never declared.

References
- https://frontendmasters.com/courses/deep-javascript-v3/undefined-vs-undeclared/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### When are global variables automatically created?
When assigning a value to an undeclared variable in non-strict mode.

References
- https://frontendmasters.com/courses/deep-javascript-v3/dynamic-global-variables/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is strict mode and when should it be used?
It is a restricted variant of JavaScript that makes code more futureproof and resilient to errors. It should be used as much as possible.

References
- https://frontendmasters.com/courses/deep-javascript-v3/strict-mode/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### In terms of grammar, what is the difference between a function declaration and a function expression?
If a statement begins with `function`, then it is a function declaration; if not, it is a function expression.

References
- https://frontendmasters.com/courses/deep-javascript-v3/function-expressions/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### In terms of scope, what is the difference between a function declaration and a function expression?
A function declaration adds its identifier to its enclosing scope. A function expression adds its identifier to its own scope.

References
- https://frontendmasters.com/courses/deep-javascript-v3/function-expressions/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What are three reasons to use named function expressions over anonymous function expressions?
It enables reliable recursion, makes stack traces debuggable, and makes self documenting code.

References
- https://frontendmasters.com/courses/deep-javascript-v3/naming-function-expressions/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### As a general rule of thumb, what is the heirarchy of best ways to create a function?
Function declarations and named function expressions are typically preferable over anonymous function expressions.

References
- https://frontendmasters.com/courses/deep-javascript-v3/function-types-hierarchy/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is the difference between lexical scope and dynamic scope?
Lexical scope is determined before runtime and dynamic scope is determined during runtime.

References
- https://frontendmasters.com/courses/deep-javascript-v3/lexical-dynamic-scope/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is the principle of least privilege and why is it useful?
It's the defensive practice that defaults to keeping everything private and only exposing what is necessary. It helps prevent name collisions and prevents misuse.

References
- https://frontendmasters.com/courses/deep-javascript-v3/function-scoping/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is an IIFE and why is it useful?
An immediately invoked function expression is a simultaneous function declaration and execution. It creates its own scope without polluting its enclosing scope.

References
- https://frontendmasters.com/courses/deep-javascript-v3/iife-pattern/
- https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is hoisting?
A metaphor for the behavior of lexical scope, especially due to it ocurring before runtime. Hoisting claims that declarations are moved to the top of their scope to explain how things like function declarations can be below where they are called yet still work.

References
- https://frontendmasters.com/courses/deep-javascript-v3/hoisting/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is the temporal dead zone?
The area between the start of a scope and the declaration of a variable declared with `const` or `let` where that variable can not be accessed because it isn't initialized yet. This is in contrast to variables declared with `var`, which can be accessed before their declaration.

References
- https://frontendmasters.com/courses/deep-javascript-v3/let-doesn-t-hoist/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is a closure?
A function that retains access to its lexical scope when executed outside that lexical scope.

References
- https://frontendmasters.com/courses/deep-javascript-v3/what-is-closure/
- https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md#what-is-a-closure-and-howwhy-would-you-use-one

**[[ ↑ ] Back to top](#javascript-notes)**

---

### What is a module?
A pattern that uses encapsulation to hide a private API while exposing a public API.

References
- https://frontendmasters.com/courses/deep-javascript-v3/module-pattern/

**[[ ↑ ] Back to top](#javascript-notes)**

---

## Objects

## ECMAScript Specification

### What are the three main parts of the ECMAScript specification?
|Topics                |Sections                                                                            |Examples                                     |
|----------------------|------------------------------------------------------------------------------------|---------------------------------------------|
|Basics                |Introduction - 9. Ordinary and Exotic Objects Behaviours                            |What is a Number?                            |
|Grammar and Semantics |10. ECMAScript Language: Source Code - 16. ECMAScript Language: Scripts and Modules |How is a `for-in` loop written and executed? |
|APIs                  |17. The Global Object - 26. Reflection                                              |What does `String.prototype.substring()` do? |

References
- https://timothygu.me/es-howto/

**[[ ↑ ] Back to top](#javascript-notes)**

---

### Abstract Operations

#### How does `ToPrimitive(input [, PreferredType])` coerce objects to primitives?
If the preferred type is string, use the `toString` method first then `valueOf` method until a primitive is returned. Otherwise, use the `valueOf` method first then `toString` method until a primitive is returned.

References
- https://tc39.github.io/ecma262/#sec-toprimitive
- https://frontendmasters.com/courses/deep-javascript-v3/abstract-operations/

**[[ ↑ ] Back to top](#javascript-notes)**

---

#### What are the `ToString(argument)` return values for each type?
|Type      |Return Values                                                |
|----------|-------------------------------------------------------------|
|String    |argument                                                     |
|Number    |`'0'`, `'Infinity'`, `'-Infinity'`, `'NaN'`, or some string  |
|Boolean   |`'true'` or `'false'`                                        |
|Undefined |`'undefined'`                                                |
|Null      |`'null'`                                                     |
|Symbol    |`TypeError`                                                  |
|Object    |`ToString(ToPrimitive(argument, hint String))`               |

References
- https://tc39.github.io/ecma262/#sec-tostring
- https://frontendmasters.com/courses/deep-javascript-v3/tostring/

**[[ ↑ ] Back to top](#javascript-notes)**

---

#### What are the `ToNumber(argument)` return values for each type?
|Type      |Return Values                                                                                                  |
|----------|---------------------------------------------------------------------------------------------------------------|
|String    |`0`, `-0`, `Infinity`, `-Infinity`, `NaN`, `0` for an empty string or one with only whitespace, or some number |
|Number    |argument                                                                                                       |
|Boolean   |`1` or `0`                                                                                                     |
|Undefined |`NaN`                                                                                                          |
|Null      |`0`                                                                                                            |
|Symbol    |`TypeError`                                                                                                    |
|Object    |`ToNumber(ToPrimitive(argument, hint Number))`                                                                 |

References
- https://tc39.github.io/ecma262/#sec-tonumber
- https://frontendmasters.com/courses/deep-javascript-v3/tonumber/

**[[ ↑ ] Back to top](#javascript-notes)**

---

#### What are the `ToBoolean(argument)` return values for each type?
|Type      |Return Values                                  |
|----------|-----------------------------------------------|
|String    |`true` unless `''`                             |
|Number    |`true` unless `0`, `-0`, or `NaN`              |
|Boolean   |argument                                       |
|Undefined |`false`                                        |
|Null      |`false`                                        |
|Symbol    |`true`                                         |
|Object    |`true`                                         |

References
- https://tc39.github.io/ecma262/#sec-toboolean
- https://frontendmasters.com/courses/deep-javascript-v3/toboolean/

**[[ ↑ ] Back to top](#javascript-notes)**

---

## Learning Resources
* [ECMAScript Specification](https://tc39.github.io/ecma262/)
* [How to Read the ECMAScript Specification](https://timothygu.me/es-howto/)
* [Frontend Masters: Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)

**[[ ↑ ] Back to top](#javascript-notes)**
