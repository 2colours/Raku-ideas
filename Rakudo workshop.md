Questions:
- are type objects guaranteed to have the same WHICH value at runtime?
- what is the lexical cope of sub MAIN? Confer https://github.com/rakudo/rakudo/issues/5090 and https://github.com/rakudo/rakudo/issues/5091
- what are separate metaobjects created for?
  - seemingly type objects, i.e $foo.HOW === $foo.WHAT.HOW?
