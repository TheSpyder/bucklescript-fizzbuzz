# BuckleScript Client-Side FizzBuzz

This demonstrates a complete build pipeline for writing client-side code in OCaml. It...

1. Compiles it to JS
2. Flattens out modules (like the OCaml stdlib and pervasives), using rollup, so browsers can run it
3. Runs it through Google's Closure Compiler to minify it

## In More Detail

We have `bsb`, the stock BuckleScript build tool, emit ES6 modules, which `rollup` consumes. Naive flattening yields 47K of JS, but rollup does some simple dead-code elimination (DCE) based on ES6 deep imports, bringing it down to 4K, and then minification tightens that to 713 bytes.

## To Build
```
npm install
```

That'll get you BuckleScript and its build tools.

```
npm run rollup
```

That'll get you the 4K JS build. To go smaller, install a modern Java, download the Closure Compiler jar, stick it in this folder, and call it "closure-compiler.jar". Then you can run...

```
npm run closure
```

To see that it works, open `index.html` in a browser, and look at the JS console, where you should see lots of fizzbuzzy log entries.

## Open Questions
* How does it work with OCaml modules from OPAM? At what layer does DCE happen there?
