# Allomorphs are a bad idea

Context: https://rakudoweekly.blog/2026/03/23/2026-12-ich-bin-ein-berliner/
- "Allomorph classes should be considered a common raku scenario."
- “I checked for Int and I got something that is not an Int (but inherits from Int)”
  - the real misunderstanding: what does "is not an Int" mean here?
  - LSP
  - "Consider this code": strawman, that's not the problem
    - in fact, the problem would be if Human overloaded in a contradicting way
    - this is a modeling question for the most part:  
      if it's a part of the invariants of animals that they can't read then either humans aren't animals, or they indeed cannot read

Red flags:
- always inherits from Str
- is silently tied to Numeric coercions (**thereby breaking Str interface already**)
Problems:
- broadly: the diamond problem
- breaking change and dubious Str return: https://github.com/rakudo/rakudo/commit/7a77b397918a345352dfdcd746b3949d3efbcf53
