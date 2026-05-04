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

Why allomorphs exist - the rhetoric and the sincere
- recommended reading: "the expression problem"
- the history and my theory
  - Perl was strong on coercions and dedicated operations
  - Raku takes this a step further with multiple dispatch: "bring your own operations" (on existing types)
  - this approach doesn't really work for class-based OO
    - your type has to be proactive about supporting an operation
    - Raku's solution: massive base classes (`Mu`, `Any`, `Cool`) the de facto cover the interfaces of particular common cases (eg. lists, strings, numbers)
      _I think this could have been done better (eg. heavier use of roles for decomposition) but doesn't cause a problem as long as there are no overlapping interfaces/name conflicts_
    - allomorphs take this a step further:
      - real OO inheritance from classes: both interfaces and behavior inherited, type checks passing
      - taking a stab at resolving overlapping interfaces/name conflicts: prefer numeric
        - "this is a number with string fallback"
        - my guess: numeric types are perceived more specific
        - _no matter the choice: this simply cannot go right_
- why are allomorphs **really** needed?
  - I don't know! :D real use-case would be appreciated
  - obvious workaround: allomorphs are strings, keep them as strings, use coercions when needed
    - coercive signatures suddenly work as expected - no need to "just" pass type checks
    - if you want eg. integer `.succ` or integer `.Bool` on a string: what's so bad about writing `$my-string.Int.succ`?

Red flags:
- always inherits from Str
- is silently tied to Numeric coercions (**thereby breaking Str interface already**)
- "is" `Str` (and another type), yet it has to bring its own `Str` coercion that isn't an identity
  - this is in fact a visible workaround: a way to opt out of allomorphs post facto
  - worse yet, it's a partial workaround: `Str($value)` doesn't have the same result, coercive signatures don't work etc.

Problems:
- broadly: the diamond problem
  - these values pass type checks without fulfilling useful invariants of that type
  - unsafe operations on `Str`: boolification, smartmatch, succ/pred
  - on `Int`, it's unsafe to make assumptions about the stringified form
  - Int-keyed hashes: if you indexed it with `IntStr`, you will never get to index it with something else
- breaking change and dubious Str return: https://github.com/rakudo/rakudo/commit/7a77b397918a345352dfdcd746b3949d3efbcf53

Bonus: guesses of `<>` quotation:
- `<i>` is a `Str`
- `<0i>`, `<1i>` are `ComplexStr`s
- `<0+0i>` etc. are `Complex`es

# Junctions and the promise of "free dinner"

```raku
sub valid-ratio($dividend, $divisor) { 1 < $dividend / $divisor < 10 }
so valid-ratio(any(10, 75, 4), all(2, 6, 7, 11)) # True ("for all $y there is an $x such as valid-ratio($x, $y)"), False wanted ("there is an $x such that for all $y, valid-ratio($x, $y)")
```
(god forbid further dimensions...)
A way out:
```raku
sub (Any $x, Mu $y) { valid-ratio($x, $y) }(any(10, 75, 4), all(2, 6, 7, 11)).so # False - $x stays the outmost layer
```
There is nothing about composition either way.
Funny negations:
```raku
my &strange = { $_ !%% 2 && $_ % 2 != 1 }
strange(1) # False
strange(2) # False
strange(1&2) # True !

my &composite-number = { !.&is-prime && $_ != 1 }
composite-number(1|4) # False !
composite-number(1&4) # True !

my &demo333 = { $_ % 5 != (3|4) }
demo333(4) # False
demo333(1) # True
demo333(1&4) # True !
demo333(1|4) # False !
```

`sub` has `Any` as default parameter type, a code block (even a pointy block!) has `Mu` as default parameter type.
