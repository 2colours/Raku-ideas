Questions:
- are type objects guaranteed to have the same WHICH value at runtime?
- what is the lexical cope of sub MAIN? Confer https://github.com/rakudo/rakudo/issues/5090 and https://github.com/rakudo/rakudo/issues/5091
- what are separate metaobjects created for?
  - seemingly type objects, i.e $foo.HOW === $foo.WHAT.HOW?
- in what scope are top-level lexical variables installed? GLOBAL, PROCESS, none, etc.
  - "my" variables aren't included, what about "our" variables?
- how to access a method (especially inherited method) as a symbol?
- what replaces World.nqp in the RakuAST implementation
- what is the difference between `local` and `lexical` (scope)?
