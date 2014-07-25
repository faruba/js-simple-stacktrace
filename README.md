# simple-stacktrace

built this from the answers here https://github.com/visionmedia/mocha/issues/545 for the purpose of changing my stack traces from things like this: 

```
1) Router POST /boards Import JSON column #1 has the right # of cards:

    AssertionError: expected 0 to equal 5
    + expected - actual

    +5
    -0

    at Context.<anonymous> (/Users/keyvan/Projects/mib/test/server/router_test.js:274:15)
    at callFn (/Users/keyvan/Projects/mib/node_modules/mocha/lib/runnable.js:223:21)
    at Test.Runnable.run (/Users/keyvan/Projects/mib/node_modules/mocha/lib/runnable.js:216:7)
    at Runner.runTest (/Users/keyvan/Projects/mib/node_modules/mocha/lib/runner.js:373:10)
    at /Users/keyvan/Projects/mib/node_modules/mocha/lib/runner.js:451:12
    at next (/Users/keyvan/Projects/mib/node_modules/mocha/lib/runner.js:298:14)
    at /Users/keyvan/Projects/mib/node_modules/mocha/lib/runner.js:308:7
    at next (/Users/keyvan/Projects/mib/node_modules/mocha/lib/runner.js:246:23)
    at Object._onImmediate (/Users/keyvan/Projects/mib/node_modules/mocha/lib/runner.js:275:5)
    at processImmediate [as _immediateCallback] (timers.js:336:15)
```

to something more like this:

```
1) Router POST /boards Import JSON column #1 has the right # of cards:

    AssertionError: expected 0 to equal 5
    + expected - actual

    +5
    -0

    at Context.<anonymous> (test/server/router_test.js:274:15)
    at processImmediate [as _immediateCallback] (timers.js:336:15)
```

which is easier to read and fits nicely without wrapping or robbing context

# usage

`npm install --save-dev simple-stacktrace`

in your tests, to get what I have above for example, you would use:

```
require('simple-stacktrace')({
  height: 4,
  node_modules: false
})
```

## options

`height`: controls the maximum height of the stack trace. defaults to `6`

`node_modules`: a `false` value hides any line that contains the string node_modules/ effectively hiding stack traces that occur outside your module. defaults to `true`
