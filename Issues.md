1. library enum used in MAIN, import from bin/ script - enum doesn't get parsed
2. built-in names cannot be used as enums in MAIN, otherwise the parsing fails silently
3. %?RESOURCES<>.IO compile-time - why couldn't it be slurped?
4. Slips
	1. X and Z disregards them
	2. they unwrap even if they are in Scalar containers - is this desirable?
5. .& detachment
	1. why is it not detachable in the first place?
	2. why does `'asd'  .comb.&dd` count as detached? Surely it couldn't be more attached to the `.comb` part?
6. `zef --help` writes to stderr
7. smartmatch to S/// _is_ useful and it _does_ work