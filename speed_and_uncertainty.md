# Uncertainty:cause of not being able to run things close to theoretical speed
source: Jeff Bezanson | Why is Julia fast?

## Total interpreter
- extreme example of a slow execution
- program is data, input is data
- step by step "execution", which is in effect just chechking to see if the program has changed
- usefull but not very often

## Common sources of uncertainty in programming languages
- variable value and type may change
    + value in static typed languages
    + value and type in dynamically typed languages
- function return type might be given by the input
- data structure updates, growth and movement
- even just a simple if condition creates uncertainty, however this one is on the level of HW and not a language (see CPU branch predictors)
- the compiler has to reason about these
    + dynamic languages such as Ruby, Python are often far from the total interpreter paradigm, as a lot of dynamic is omptimized away
    + programs are repetetive (inner loops)
    + JITs for JS exploit the uncertainty by compiling for probable version and fallbacking to the actuall case, just before the wall is hit
        * in JS there is a "hack", which forces variables to be int32 by using "|0" (or zero) to force the JIT to see variables as int32s
        * an example of throwing abstractions in order to run quickly
        * that's why we need efficient abstractions -> Julia

## Removing uncertainty in Julia
- systematic vocabulary of types (want to "or zero" everything, not just integers)
- type assertions and conversion
- typed locations
    + more efficient layout and access
    + not just pointer to a wrapper with type
- typed based dispatch
    + more predictable control flow once in a function with known arguments
- "Makes it easy to write programs that are easy to statically analyze." - Oscar Blumberg
- type inference causes variables to lose they dynamics, however removes uncertainty down the line
- specialization based on infered types
    + for data -> makes memory layout easier to comprehend
    + for code -> allows to use direct call or inlining
    + it may also be used for special values of arguments
- types don't have to be just data types like Int32, but also more complicated structures 














