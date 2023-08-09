# LabVIEW_Expressions

LabVIEW library to evaluate numerical and conditional expressions at run-time.

## Getting Started

Clone the repository and run the `/Examples/Expressions Example.vi` to see how expressions are evaluated at run-time.

![Example](/Images/Example.png)

![Example](/Images/Example-Diagram.png)

## Usage

Expression statements are useful in interpreter languages (e.g. Python, Ruby) since they can be modified and evaluated at run-time. LabVIEW does not have a run-time interpreter so I created one. This library tokenizes an **Expression** statement string into postfix operations before evaluating the expression numerically at run-time.

Expressions can be nested in paratheses `'(...)'`, support
numerical `'(a + b * c)'`, and boolean/conditional `'(d or e) and not f or a > 0.4'` statements. Statements can contain one or more
operations, literals, or variables.

```
Numerical Expression Example:

((a * b) / c) * (a - b)
```

```
Boolean/Conditional Expression Example:

(d or e) and not f or (a >= 0.5)
```

Literals and variables can be Booleans, I32s, U32s, and DBLs which are all converted to DBLs before evaulation.

Variables are defined as a `name:value` pairs and converted to a 1D array of string names and DBL values. For example, variables could be control labels and values (shown in the example), or shared variable names and values, a map, or any other named pair set. The only requirement is that the variable's name and value are positionally indexed the same:

`[a:True, b:False] -> names=['a','b'], values=[True,False]`

This creates a variable lookup table using the index as the
reference, allowing the evaluator to map variables faster, and remove the variable names from the expression altogether.

### Features

Expressions can be nested using parentheses `(a or b) and (c or d)`.

Expressions can use pythonic nomenclature `(a and b or not c)` or C++ nomenclature `(a && b || !c)`.

Expressions support basic arithmetic `(+ - * / %)`

Expressions support boolean operations and conditionals: `(and or not == != > < >= <=)`

### Supports:

```
AND:          and | && | &
OR:           or | '||' | '|'
NOT:          not | !
EQUAL:        ==
NOT EQUAL:    !=
LESS THAN:    <
GREATER THAN: >
LTE:          <=
GTE:          >=
PLUS:         +
MINUS:        -
MULTIPLY:     *
DIVIDE:       /
MODULUS:      %
PARENTHESES:  (..)
LITERAL:      Boolean | DBL | I32 | U32
VARIABLE:     [A-Za-z_][A-Za-z0-9_]*
```

_Note: Bit-wise and assignment operations are not supported._

### Examples

`(a + b) * a - (c / b)`

`(a > b or c <= 0) and d or e`

`(d or not e) and f or (a <= b * c)`

`(((d or e) or f) and e)`

## Support

The future goal is to develop a mini-interpreter that support
assignments, loops, if-then statements, etc. for a
run-time scripting engine built entirely in LabVIEW.

Open a ticket to bug fixes or feature requests.
