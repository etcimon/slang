# Execution path

The driver is `source/driver` (`Driver`, used by `sv-elab`'s
`slang_frontend.cc`).

1. `source/parsing` and `source/syntax` turn text into a `SyntaxTree`.
   The lexer and parser are here. A syntax node is not yet typed.
2. `source/compiler` binds names and builds the AST
   (`Compilation`, symbols under `source/ast`).
3. Elaboration evaluates parameters, generates, and instance arrays into
   instance symbols. The visitor in `sv-elab` starts after this step.
4. Diagnostics (`DiagnosticEngine`) collect errors. They are not the
   netlist.

There is no timing graph. There is no liberty.

An instance array or a generate loop that exceeds the unroll budget fails
the compilation. It does not become a black box the timer can ignore.
CVA6's `g6lc_iq` with `NR_SB_ENTRIES=64` is the case that exceeds slang's
default unroll. The Yosys `read_slang` invocation keeps a high unroll limit
for that reason.
