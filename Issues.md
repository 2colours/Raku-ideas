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
14. `$<a b>` should behave like `$[0, 1]`
