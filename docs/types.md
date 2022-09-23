# Types

## Basic Types

The Joy programming language defines several basic types.

| Type | Description |
|------|-------------|
| `bool` | Boolean (`true` or `false`) |
| `char` | A single Unicode character |
| `int8` | 8-bit signed integer |
| `int16` | 16-bit signed integer |
| `int` | 32-bit signed integer |
| `int64` | 64-bit signed integer |
| `byte` | 8-bit bitmask |
| `byte16` | 16-bit bitmask |
| `byte32` | 32-bit bitmask |
| `byte64` | 64-bit bitmask |
| `float32` | 32-bit floating point number |
| `float64` | 64-bit floating point number |

## Type Conversions

In Joy, there are no implicit conversions between types.
For example, attempting to assign a `byte` to an `int` results in a compilation error.
Instead, an explicit conversion must be done, such as by using the `byte` type's `toInt32()` method.

The one exception is type promotion of the integer types.
For example, an `int8` can be assigned to an `int64`.
The opposite, however, is a compilation error.
For example, an `int64` can be assigned to an `int8`.
Instead, an explicit conversion would be needed,
such as by using the `int64` type's `clampToInt8()` method.

This requirement helps to avoid programming errors where type conversions may be unintentional,
especially those that would be lossy, such as converting from `int64` to `int8`.
Being explicit about type conversions also improves code readability
because it is clear that a conversion is happening and that the original developer intended it.

Moreover, some types can be converted to other types using multiple algorithms.
For example, converting a `byte` to an `int` could be done
by interpreting the byte as a 2's-complement signed integer, or as an unsigned integer.

As a natural consequence, there is no concept of "truthy" or "falsy".
Some other programming languages treat special values of some types
as "false" in a boolean context, like an `if` statement.
Python and JavaScript, for example, treat the number `0` and the empty string as "false",
and all other numeric values and non-empty strings as "true".
In Joy, any value must be converted to a `bool` to be used in a boolean context.

## The `bool` Type

The `bool` type has exactly two possible values: `true` and `false`.
Both `true` and `false` are reserved words in the Joy programming language.
There are no conversions available from `bool` to any other type.

## The `char` Type

The `char` type stores a single Unicode character.
It cannot be used in any mathematical calculations;
for example, you cannot "add" two `char` values.

One common conversion from `char` is to `int16` using
the `char` type's `codePoint` attribute,
which is the character's Unicode code point.

Joy only supports the Unicode "Basic Multilingual Plane" (BMP);
therefore, all `char` values have a code point that fits into an `int16` value.

## The `int`, `int8`, `int16`, and `int64` Types

The integer types are not very surprising, if you're familiar with integer types in other languages.
The "default" integer type is `int`, which is a 32-bit integer. If in doubt, this is probably the
right type for you. All containers in Joy's standard library use `int` as the size.

The integer types support the following arithmetic operators:
| Operator | Name |
|----------|------|
| `+` | addition |
| `-` | subtraction |
| `*` | multiplication |
| `/` | floating point division |
| `//` | floor division |
| `**` | exponent |
| `%` | modulo |

The integer types support the following assignment operators:
| Operator | Meaning |
|----------|------|
| `=` | assign |
| `+=` | `x += y` means `x = x + y` |
| `-=` | `x -= y` means `x = x - y` |
| `*=` | `x *-*= y` means `x = x * y` |
| `/=` | `x /= y` means `x = x / y` |
| `//=` | `x //= y` means `x = x // y` |
| `**=` | `x **= y` means `x = x ** y` |
| `%=` | `x %= y` means `x = x % y` |
| `++` | `x++` means `x += 1` |
| `--` | `x--` means `x -= 1` |
