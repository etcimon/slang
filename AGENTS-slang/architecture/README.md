# slang architecture notes

slang compiles SystemVerilog to an elaborated AST. `sv-elab` walks that AST.
OpenSTA does not.

| Note | What it answers |
|---|---|
| [EXECUTION.md](EXECUTION.md) | Parse, bind, elaborate |
| [DATA.md](DATA.md) | Syntax tree versus AST versus instances |
| [OPPORTUNITIES.md](OPPORTUNITIES.md) | Unroll, lookup, and what not to cache |

Fork: `https://github.com/etcimon/slang`, branch `g6lc`, at the commit
`sv-elab` already pins. No algorithm edit on that branch yet.
