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
    - [How can coercion and edge cases be handled in code?](#how-can-coercion-and-edge-cases-be-handled-in-code)
  - [Scope](#scope)
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
|Primitive or Built-In | Type     |`typeof` Return Values     |Distinct Values                             |
|----------------------|----------|---------------------------|--------------------------------------------|
|Primitive             |String    |`'string'`                 |                                            |
|Primitive             |Number    |`'number'`                 |`0`, `-0`, `Infinity`, `-Infinity`, `NaN`   |
|Primitive             |Boolean   |`'boolean'`                |`true` or `false`                           |
|Primitive             |Undefined |`'undefined'`              |`undefined`                                 |
|Primitive             |Null      |`'object'`                 |`null`                                      |
|Primitive             |Symbol    |`'symbol'`                 |                                            |
|Built-In              |Object    |`'object'` or `'function'` |                                            |

References
- https://tc39.github.io/ecma262/#sec-ecmascript-language-types
- https://tc39.github.io/ecma262/#sec-typeof-operator

[[ ↑ ] Back to top](#questions)

---

### Are types attached to variables or values?
Values have types, not variables.

References
- https://frontendmasters.com/courses/deep-javascript-v3/primitive-types/

[[ ↑ ] Back to top](#questions)

---

### Which types are immutable and which types are mutable?
All primitive types are immutable and the built-in Object type is mutable.

References
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Primitive_values

[[ ↑ ] Back to top](#questions)

---

### What is the difference between a variable whose value is `undefined` or `null`? How can they be checked?
When a variable is declared with `var` or `let` and not assigned a value, it has the value `undefined`.

Both `undefined` and `null` can be checked with the equality operators, but `null` can not be checked with `typeof`.

References
- https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md#whats-the-difference-between-a-variable-that-is-null-undefined-or-undeclared-how-would-you-go-about-checking-for-any-of-these-states

[[ ↑ ] Back to top](#questions)

---

### What is `NaN` and when does it occur? How can it be checked?
`NaN` represents an invalid number that arises from invalid numerical operations, like trying to coerce an incompatible value to a number.

`NaN` is the only value that is not equal to itself so the inequality operators can check for it. There's the more semantic `isNaN` function but it can return unexpected results due to coercing its argument to a number. So the preferred method is `Number.isNaN()`, which checks for `NaN` without coercion.

References
- https://frontendmasters.com/courses/deep-javascript-v3/nan-isnan/

[[ ↑ ] Back to top](#questions)

---

### Why is there `-0`, how can it be checked, and how can it be useful?
JavaScript uses the IEEE 754 standard so it requires all numbers to be signed.

None of the comparison operators can distinguish `-0`, so use `Object.is()` to check for it.

The signed zero is just extra data. For something like stock trends where trends may decrease or increase before flatlining, the negative or positive zero can indicate if the trend was last increasing or decreasing.

References
- http://2ality.com/2012/03/signedzero.html
- https://frontendmasters.com/courses/deep-javascript-v3/negative-zero/

[[ ↑ ] Back to top](#questions)

---

### What is boxing?
'Boxing' refers to the implicit coercion of primitives into objects when trying to access their properties and methods.

References
- https://frontendmasters.com/courses/deep-javascript-v3/boxing/

[[ ↑ ] Back to top](#questions)

---

### Why is there a bias against implicitness and what's a better way to think about it?
Implicit mechanisms are associated with being bad because they do things behind the scenes. Implicitness is better thought of as abstraction. While it isn't always good, it can be necessary because it hides unneccesary details and allow the reader to focus on what's important.

References
- https://frontendmasters.com/courses/deep-javascript-v3/implicit-coercion/

[[ ↑ ] Back to top](#questions)

---

### How are the abstract and strict equality operators alike and different?
If the types are the same, they do the same thing. If not, the abstract equality operator performs coercion. Specifically if the types are `null` and `undefined`, it will return `true` or try to convert each type into a number.

References
- https://tc39.github.io/ecma262/#sec-abstract-equality-comparison
- https://frontendmasters.com/courses/deep-javascript-v3/double-equals-summary/
- https://dorey.github.io/JavaScript-Equality-Table/

[[ ↑ ] Back to top](#questions)

---

### How can coercion and edge cases be handled in code?
By adopting a coding style that makes types plain and obvious.

References
- https://frontendmasters.com/courses/deep-javascript-v3/intentional-coercion/

[[ ↑ ] Back to top](#questions)

---

## Scope

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

[[ ↑ ] Back to top](#questions)

---

### Abstract Operations

#### How does `ToPrimitive(input [, PreferredType])` coerce objects to primitives?
If the preferred type is string, use the `toString` method first then `valueOf` method until a primitive is returned. Otherwise, use the `valueOf` method first then `toString` method until a primitive is returned.

References
- https://tc39.github.io/ecma262/#sec-toprimitive
- https://frontendmasters.com/courses/deep-javascript-v3/abstract-operations/

[[ ↑ ] Back to top](#questions)

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

[[ ↑ ] Back to top](#questions)

---

#### What are the `ToNumber(argument)` return values for each type?
|Type      |Return Values                                                                                             |
|----------|----------------------------------------------------------------------------------------------------------|
|String    |`0` for an empty string or one with only whitespace, `-0`, `Infinity`, `-Infinity`, `NaN`, or some number |
|Number    |argument                                                                                                  |
|Boolean   |`1` or `0`                                                                                                |
|Undefined |`NaN`                                                                                                     |
|Null      |`0`                                                                                                       |
|Symbol    |`TypeError`                                                                                               |
|Object    |`ToNumber(ToPrimitive(argument, hint Number))`                                                            |

References
- https://tc39.github.io/ecma262/#sec-tonumber
- https://frontendmasters.com/courses/deep-javascript-v3/tonumber/

[[ ↑ ] Back to top](#questions)

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

[[ ↑ ] Back to top](#questions)

---

## Learning Resources
* [ECMAScript Specification](https://tc39.github.io/ecma262/)
* [How to Read the ECMAScript Specification](https://timothygu.me/es-howto/)
* [Frontend Masters: Deep JavaScript Foundations, v3](https://frontendmasters.com/courses/deep-javascript-v3/)

[[ ↑ ] Back to top](#questions)
