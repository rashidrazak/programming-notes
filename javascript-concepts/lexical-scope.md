# JavaScript Lexical Scope

Lexical scope is a scope model that is used by JavaScript language.
Some other languages use dynamic scope, which is totally different when compared to lexical scope.
In lexical scope, the scope is defined at `lexing` time.

## What is lexing time?

Commonly, source code compilation consists of these 3 steps/phases:

  1. Lexing
  2. Parsing
  3. Generating Executables

Lexing time is actually a phase where text (stream of characters) being converted to stream of tokens.
One token can be represented by multiple charaters. Take this source code for example:

```javascript
function a() {
  var a = 1;
}
```

could be transformed to a stream of tokens similar to this:

```
KFunction, Identifier("a"), LBracket, KVar, Identifier("a"), Assignment, Number(1), Semicolon, RBracket
```

Lexing phase is important for:

  1. Simplifying syntax grammar that is used for parsing
  2. Perform uniformization of code such as removing comments and replacing escape characters
  3. etc.



## References

[Astronaut Web Co. - What is Lexical Scope Anyway?](https://astronautweb.co/javascript-lexical-scope/)
[Medium.com - Javascript evaluator part 1: Lexing](https://medium.com/@retep007/javascript-lexing-for-high-performance-f9a800ec930d)
