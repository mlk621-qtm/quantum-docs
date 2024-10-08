---
author: bradben
description: Learn about the different types of literals in the Q# programming language.
ms.author: brbenefield
ms.date: 08/15/2024
ms.service: azure-quantum
ms.subservice: qsharp-guide
ms.topic: reference
no-loc: ['Q#', '$$v']
title: Literals in Q#
uid: microsoft.quantum.qsharp.valueliterals
---

# Literals

## Unit literal

The only existing literal for the [`Unit` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) is the value `()`.

The `Unit` value is commonly used as an argument to callables, either because no other arguments need to be passed or to delay execution. It is also used as return value when no other value needs to be returned, which is the case for unitary operations, that is, operations that support the `Adjoint` and/or the `Controlled` functor.

## Int literals

Value literals for the [`Int` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) can be expressed in binary, octal, decimal, or hexadecimal representation. Literals expressed in binary are prefixed with `0b`, with `0o` for octal, and with `0x` for hexadecimal. There is no prefix for the commonly used decimal representation.

| Representation | Value Literal |
| --- | --- |
| Binary | `0b101010` |
| Octal | `0o52` |
| Decimal | `42` |
| Hexadecimal | `0x2a` |

## BigInt literals

Value literals for the [`BigInt` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) are always postfixed with `L` and can be expressed in binary, octal, decimal, or hexadecimal representation. Literals expressed in binary are prefixed with `0b`, with `0o` for octal, and with `0x` for hexadecimal. There is no prefix for the commonly used decimal representation.

| Representation | Value Literal |
| --- | --- |
| Binary | `0b101010L` |
| Octal | `0o52L` |
| Decimal | `42L` |
| Hexadecimal | `0x2aL` |

## Double literals

Value literals for the [`Double` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) can be expressed in standard or scientific notation.

| Representation | Value Literal |
| --- | --- |
| Standard | `0.1973269804` |
| Scientific | `1.973269804e-1` |

If nothing follows after the decimal point, then the digit after the decimal point may be omitted. For example, `1.` is a valid `Double` literal and the same as `1.0`.

## Bool literals

Existing literals for the [`Bool` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) are `true` and `false`.

## String literals

A value literal for the [`String` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) is an arbitrary length sequence of Unicode characters enclosed in double quotes.
Inside of a string, the back-slash character `\` may be used to escape
a double quote character, and to insert a new-line as `\n`, a carriage
return as `\r`, and a tab as `\t`.

The following are examples for valid string literals:

```qsharp
"This is a simple string."
"\"This is a more complex string.\", she said.\n"
```

Q# also supports *interpolated strings*.
An interpolated string is a string literal that may contain any number of interpolation expressions. These expressions can be of arbitrary types.
Upon construction, the expressions are evaluated and their `String` representation is inserted at the corresponding location within the defined literal. Interpolation is enabled by prepending the special character `$` directly before the initial quote, with no white space between them.

For instance, if `res` is an expression that evaluates to `1`, then the second sentence in the following `String` literal displays "The result was 1.":

```qsharp
$"This is an interpolated string. The result was {res}."
```

## Qubit literals

No literals for the [`Qubit` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) exist, since quantum memory is managed by the runtime. Values of type `Qubit` can hence only be obtained via [allocation](xref:microsoft.quantum.qsharp.quantummemorymanagement#quantum-memory-management).

Values of type `Qubit` represent an opaque identifier by which a quantum bit, or *qubit*, can be addressed. The only operator they support is [equality comparison](xref:microsoft.quantum.qsharp.comparativeexpressions#equality-comparison). For more information on the `Qubit` data type, See [Qubits](xref:microsoft.quantum.qsharp.quantumdatatypes#qubits).

## Result literals

Existing literals for the [`Result` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) are `Zero` and `One`.

Values of type `Result` represent the result of a binary quantum measurement.
`Zero` indicates a projection onto the +1 eigenspace, `One` indicates a projection onto the -1 eigenspace.

## Pauli literals

Existing literals for the [`Pauli` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) are `PauliI`, `PauliX`, `PauliY`, and `PauliZ`.

Values of type `Pauli` represent one of the four single-qubit [Pauli matrices](https://en.wikipedia.org/wiki/Pauli_matrices), with `PauliI` representing the identity.
Values of type `Pauli` are commonly used to denote the axis for rotations and to specify with respect to which basis to measure.

## Range literals

Value literals for the [`Range` type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) are expressions of the form `start..step..stop`, where `start`, `step`, and `end` are expressions of type `Int`. If the step size is one, it may be omitted. For example, `start..stop` is a valid `Range` literal and the same as `start..1..stop`.

Values of type `Range` represent a sequence of integers, where the first element in the sequence is `start`, and subsequent elements are obtained by adding `step` to the previous one, until `stop` is passed.
`Range` values are inclusive at both ends, that is, the last element of the range is `stop` if the difference between `start` and `stop` is a multiple of `step`.
A range may be empty if, for instance, `step` is positive and `stop < start`.

The following are examples for valid `Range` literals:

- `1..3` is the range 1, 2, 3.
- `2..2..5` is the range 2, 4.
- `2..2..6` is the range 2, 4, 6.
- `6..-2..2` is the range 6, 4, 2.
- `2..-2..1` is the range 2.
- `2..1` is the empty range.

For more information, see [Contextual expressions](xref:microsoft.quantum.qsharp.contextualexpressions#contextual-and-omitted-expressions).

## Array literals

An [array](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) literal is a sequence of zero or more expressions, separated by commas and enclosed in brackets `[` and `]`; for example, `[1,2,3]`.
All expressions must have a [common base type](xref:microsoft.quantum.qsharp.subtypingandvariance#subtyping-and-variance), which is the item type of the array. If an empty array is specified with `[]`, a type annotation may be needed for the compiler to determine the appropriate type of the expression.

Arrays of arbitrary length may be created using a sized-array expression.
Such an expression is of the form `[expr, size = s]`, where `s` can be any expression of type `Int` and `expr` is evaluated to a value that will be the items of the array repeated `s` times. For example, `[1.2, size = 3]` creates the same array as `[1.2, 1.2, 1.2]`.

## Tuple literals

A [tuple](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) literal is a sequence of one or more expressions of any type, separated by commas and enclosed in parentheses `(` and `)`. The type of the tuple includes the information about each item type.

| Value Literal | Type |
| --- | --- |
| `("Id", 0, 1.)` | `(String, Int, Double)` |
| `(PauliX,(3,1))` | `(Pauli, (Int, Int))` |

Tuples containing a single item are treated as identical to the item itself, both in type and value, which is called [singleton tuple equivalence](xref:microsoft.quantum.qsharp.singletontupleequivalence#singleton-tuple-equivalence).

Tuples are used to bundle values together into a single value, making it easier to pass them around. This makes it possible for every callable to take exactly one input and return exactly one output.

## Literals for struct types

Values of a [struct type](xref:microsoft.quantum.qsharp.typesystem-overview#available-types) are assigned when you create a new instance, using either the `new` statement or the constructor created by the compiler.

For example, if `IntPair` is a `struct` defined as 

```qsharp
struct IntPair {
    num1 : Int,
    num2 : Int,    
}
```

then you create a new instance and assign values using

```qsharp
let MyPair = new IntPair { num1 = 5, num2 = 7 };
```

or 

```qsharp
let MyPair = IntPair(5, 7);
```

## Operation and function literals

Anonymous operations and functions can be created using a [lambda expression](xref:microsoft.quantum.qsharp.closures#lambda-expressions).

