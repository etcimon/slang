# Opportunities

Profile elaboration on a CVA6 file, not a gate-level STA run.

- Name lookup is already hashed. The expensive part of a large generate is
  the number of instances created, which is the unroll. Cutting the unroll
  limit changes the design or fails. It is not a speedup.
- The constant evaluator folds parameters. Caching a folded constant by
  `(expression id, parameter values)` is O(1) only if the key is the
  elaborated symbol, not a printed string. A string key allocates and
  compares characters.
- Do not bit-blast packed structs in slang to make later STA faster. STA
  never sees this AST. The gate netlist is produced by synthesis after
  `sv-elab` emits RTLIL.
- Diagnostics: keep the range, format on print. Same rule as not calling
  `fmt::format` in a visitor that runs once per statement.
