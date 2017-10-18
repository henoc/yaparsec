# yaparsec

Yet another parser combinator.  
The class structure is referenced by [scala-parser-combinators](https://github.com/scala/scala-parser-combinators).

## Installing

```bash
npm install yaparsec
```

## Useage

typescript:  

```typescript
import { literal } from "yaparsec";

// literal parsing
const abcParser = literal("abc");
const parsedResult = abcParser.of("abcdefg"); // input: "abcdef"
console.log(parsedResult); // Success { rest: 'defg', result: 'abc' }
```

Implemented functions are based on PEG (Parsing Expression Grammar). You can find more examples in test files.

## Operators

`p, q: Parser`  

| function | description |
|:---------|:------------|
|p.of(input)|take input for parser `p`|
|p.map(fn)|map the parse result of `p` with `fn`|
|p.then(() => q)|sequence parser|
|p.or(() => q)|ordered choice parser (try `q` only if `p` fails)|
|p.rep()|`p*`|
|p.rep1()|`p+`|
|p.rep1sep(() => q)|`p(qp)*`|
|p.opt()|`p?`|
|p.not()|success if input does **not** start with `p`|
|p.guard()|success if input starts with `p`, without consuming input|
|p.saveR(() => q)|same as sequence, but discard left result (~>)|
|p.saveL(() => q)|same as sequence, but discard right result (<~)|
|p.into(fq)|2nd parser depends on the result of the 1st parser (>>)|
|seq(...ps)|sequence parser that has many sub parsers|
|lt(str)|parse specified string `str`|
|r(regexp)|parse any string match `regexp`|
|decimal|decimal number parser|

## License

Yaparsec is available under the MIT license.
