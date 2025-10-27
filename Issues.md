1. **(OPENED)** library enum used in MAIN, import from bin/ script - enum doesn't get parsed
2. **(OPENED)** built-in names cannot be used as enums in MAIN, otherwise the parsing fails silently
3. %?RESOURCES<>.IO compile-time - why couldn't it be slurped?
4. Slips
	1. X and Z disregards them
	2. they unwrap even if they are in Scalar containers - is this desirable?
5. .& detachment
	1. why is it not detachable in the first place?
	2. why does `'asd'  .comb.&dd` count as detached? Surely it couldn't be more attached to the `.comb` part?
6. **(OPENED)** `zef --help` writes to stderr
7. **(OPENED)** smartmatch to S/// _is_ useful and it _does_ work
	- exactly as `$foo ~~ /regex/` or `$foo ~~ m/regex/` would work
		- sets the $/ match variable
		- returns with the result of substitution
	- `given` or `with` is not sufficient replacement because there can be only one of them per statement
	- `$foo ~~ S/a/b/ ~~ S/c/d/` is actually a good-looking paradigm
	- alas, the current behavior is documented: https://docs.raku.org/language/regexes#Substitution -> I propose the adoption as well
		- either deleting the note plain and simple
		- or also adding that it works like `$foo ~~ /regex/`, setting $/
8. **(OPENED)** `sub demo(|c, :$name) { say c; say $name; }; demo(1);`
	- "expected 1 positional but got 1" WTF?
	- seems like it actually expects no positionals at all
	- how does this work?
9. **(OPENED)** `().min == Inf && ().max == -Inf` ?
10. `ACCEPTS(Match:D:)` is a hack
	- confer "smartmatch to S/// _is_ useful and it _does_ work" issue
	- in order to support s/// and m// (perhaps tr/// as well?), smartmatching to a match object always returns the match object
	- this is a more serious and fundamental misuse of smartmatch than any "regex operator"
11. `~~` order of argument evaluation:
	- precedence: like `==`
	- when executed:
		1. takes the LHS value
		2. _binds `$_` to the LHS, inside the RHS **expression**_
		3. evaluates and takes the RHS value
	- pro: very clever
	- contra:
		- hard to describe: specify, document, explain
			- maybe referring to `&&` and `||` (short-circuiting) can help
		- hard to implement?
			- does it contribute to the Rakudo-as-Raku merger of implementation and specification?
12. `my Int &var` things:
	- valid, designed concept backed up by `Callable[::T]` - need to be documented
	- `Callable[::T]` itself needs to be documented: based on the declared return value of the Callable instance
	- The sole fact that Callable can be parameterized and what that does, needs to be documented.
	-  `my Int &var = -> --> Int { 6 }` fails; this is probably a bug, file a Rakudo issue for this. 
	- `my Int &var` defaults to unparameterized Callable which is bogus typing and my first bet would be that it's also a bug - file a Rakudo issue for it. `Callable[Int]` should be sufficient for a default value.
13. `Nil` and `min` / `max`:
	- `Nil` acts
		- as 0 for numbers
		- as the string `"Nil"` for strings
		- as `(0, )` (???) for lists
	- needs consistent semantics, possibly error
 	- **UPDATE**: without code snippets, I have no idea what I meant here, I cannot reproduce anything like this, even with older Rakudo versions
14. `$<a b>` should behave like `$[0, 1]`
15. **(OPENED)** Handling of non-breaking spaces when splitting to words
	- https://docs.raku.org/language/traps#___top "using Set subroutines (...)" part
		- it produces `"a b"` and returns `False` for both code examples
		- ... for all bisectable6 versions
	- https://docs.raku.org/language/quoting#index-entry-quote_%3C%3C_%3E%3E-quote_%C2%AB_%C2%BB-Word_quoting_with_interpolation_and_quote_protection:_%C2%AB_%C2%BB
		- seems to work the same way as `<<>>` but that way also doesn't match the output in the docs: `("42 b", "c ")`
	- reason: non-breaking space!
	- https://docs.raku.org/language/quoting#Word_quoting:_qw says:
	  
	  > The `:w` form, usually written as `qw`, splits the string into "words". In this context, words are defined as sequences of non-whitespace characters separated by whitespace.  

	- [words](https://docs.raku.org/routine/words) does seem to match this description and produce the supposed output with non-breaking spaces as well
	- both can make sense but which one is correct?
16. `Bool(function-returning-native-int)` regression:
	 - bisects to this: https://github.com/rakudo/rakudo/commit/6bd955e6ea131dee6794256f5bf0da8018c3e095
	 - tldr the return value was boxed; it turned unboxed but not quite enough to work
 17. assignment of native types:
	 - a native `int` cannot be assigned using a string literal, even if that string literal contains an integer
	 - a native `int` is perfectly content with a native `str` variable on the right handside: voluntaristic integer parsing will happen; even complete nonsense can give a 0 return value
18. parsing of "unary `&`"
	- ~~`say &5` yields `(Any)` with RakuAST frontend and `Nil` with legacy frontend~~ seems to be fixed now
	- `say &(5)` yields 5 for both, RakuAST frontend sees it as an item contextualizer
19. `utf` buffers and `Stringy`
	- `utf8` and the likes are `Stringy`
	- expectation: their `Stringy` method will return them
	- reality: their `Stringy` method _upgrades_ to `Str`
	- is there a practical reason? can it be changed?
20. support for `&infix:<~^>` on various `Blob`s
	- in theory, all `Blob`s can support this operator
	- in practice, `utf` buffers upgrade to `Str`, see 19.
	- if there is one item, `Stringy` is called which doesn't work for most `Blob` types
	- if there are no items, the default value is the empty string that won't work well with `Blob` types (probably with any non-`Str` types)
21. `SignedBlob` and `UnsignedBlob` publicity
	- should they remain implementation details?
		- if yes, can we gist them in a way that points it out?
	- if no: document them, spec them
22. **(OPENED)** `Target(SourceSubset)` evaluation order
	- ~~seems that the coercion happens _before_ any checks (for the subset) would be performed?~~
	- correction: multi dispatch tries the source type object if there isn't a `:D` constraint - according to vrurg, this is an optimizer bug
23. apparently all roles are `Cool`
	- tested with smartmatch
	- the underlying NQP op reports the same
	- https://github.com/rakudo/rakudo/commit/0035ddb46de48be17492c4a11be3d4070b30077f deliberately introduced it but why for `Cool`?
24. dependency management doesn't make a lot of sense at the moment
	- the unit of a dependency is a module
	- the unit of sharing code in a managed manner is a distribution
	- a distribution can contain any number of modules and it's identified with metadata
	- the metadata of a module is not taken into account while installation
	- this leads to the bizarre situation that a module cannot be properly identified without knowing the distribution
	- different motives for creating a distribution:
		- install scripts -> won't be depended upon but needs to be installable via dist id
		- release some modules with tightly coupled code -> perhaps there is no point in pretending that one only depends on the module when the rest of the dist could not be separated
		- bundling modules for more convenient sharing -> it would make sense to actually allow independent metadata for the modules
	- in any case - it doesn't seem reasonable to make dependencies a combo of module metadata (name) and dist metadata (auth, version, etc.)
25. **(OPENED)** `token`s and capture groups
	- `my token inQuote { \' .*? \' }; say "'Hello World'" ~~ / <inQuote> /` matches
	- `my token inQuote   {  \' <(.*?)> \' }; say "'Hello World'" ~~ / <inQuote> /` (mind the match delimeters) also matches
	- `my token inQuote { \' (.*?) \' }; say "'Hello World'" ~~ / <inQuote> /` (mind the positional capture instead of the match delimeters) doesn't match!
	- why? is this intended or a bug?
26. `my Real() $demo = 'almafa'` throws, yet `'almafa' ~~ Real()` succeeds
	- seems to work with a great variety of type checks, possibly all coercion types where the source type is okay
	- given example bisects to https://github.com/rakudo/rakudo/commit/f2d73287f95ad6fa9eba8856ad15f3e8f9076d6e
27. a `Pair` value cannot be bound to a positional in a subsignature
	- `my $default = 12 => 34; my :($pair) := ($default,)` will fail: `Too few positionals passed to '<unit>'; expected 1 argument but got 0`
	- succeeds with non-`Pairs`
	- even binding the right handside to a `Slip` won't help
 	- possibly related to https://github.com/rakudo/rakudo/issues/4534
  	- assumed to be related: https://github.com/rakudo/rakudo/issues/5718
28. `say: "d", 5` - why is that a `Label`?
	- reading both https://docs.raku.org/language/control#LABELs and especially https://docs.raku.org/type/Label, it seems that `Label`s are only for loops
 	- yet the parsing shows that we created a perfect label for an expression
  	- either the docs are wrong or this should be an error
   	- should be easy to ban this in RakuAST
29. `use 6.e.PREVIEW; if 1..0 { say 'This shouldn't be True.' }` fires
	- seems like `if` uses an opcode for coercion and that doesn't respect the setting
	- mind you: `so 1..0` would have been `False`
