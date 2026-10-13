# Data and cost

## Syntax tree

Nodes are arena-allocated and immutable after parse. A token is an offset
into the source buffer, not an owned string. Copying a syntax node by value
is wrong. Holding a pointer into the arena is O(1) and dies with the
compilation.

## Symbols

Lookup is a hash from name to symbol in the scope. That is O(1) expected.
A linear scan of a scope's members is for iteration, not for lookup. Do not
add a second name map in `sv-elab` for symbols slang already hashed.

## Instances

An elaborated instance is a symbol with a parameter value set and port
connections. Port connections are expressions. Width is on the type. A wide
packed value is a bit vector in the constant evaluator, not one node per
bit. Splitting it into bits here duplicates work the Yosys `SigMap` would
then have to undo.

## Diagnostics

A diagnostic is a code plus source ranges. Rendering it formats text.
Rendering every diagnostic during a successful compile is wasted. The engine
can store them unformatted until something prints.
