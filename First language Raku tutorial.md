Programs in a nutshell:
- input
- computation
- output

Of course they don't have to happen only once/in a strict order.


The nature of the computation: two approaches
a. the input is reflected in inner state changes - "imperative style"
b. the input is transformed into the output using pure functions - "functional style"

 Metaphysical background:
 - in math, `a = a + 1` doesn't make sense
 - however, in nature, things are in constant change
	 - my age changes
	 - well, my birth date doesn't...
	 - ... but then time itself does
 - we assume that the laws of physics don't change and numbers definitely don't
 - Ship of Theseus will return a couple of times

Practical consequences:
- FP
	- data dependencies are more transparent -> better concurrency
- IP
	- the basic paradigm of CPU's -> easy to make fast

Let's start with values:
- most important property: cannot change (*plain values*)
- types (in Raku)
	- Numeric: Rat, FatRat, Complex, Num, Int...
	- Textual: Str
	- composite structures (if they consist of plain values only)
		- List, Map
			- only according to my definition - doesn't behave like that
			- there is ValueList and ValueMap :)
		- Setty types: Set, Bag

Terms:
- declared with \
	- disclaimer: among other things - note to self: needs a better name
- referenced without any prefix(=sigil)
- bound to the right handside
	- can be seen as alias when used with plain values

First runtime interactions:
- `prompt` subroutine

Installation:
- using rakubrew on Ubuntu, WSL
- major OS'es are supported
- please report issues you encounter


Calculations in the REPL:
- TODO: a show-off of some operators on numbers and strings
	- basic numeric operators
	- some method calls
	- ~, x
	- comparisons: at least numeric and textual