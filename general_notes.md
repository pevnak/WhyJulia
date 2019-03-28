# Notes
- compare C, Julia, Python next to each other
    + simple to more complicated examples
    + show first Julia, which is closer to C and then Julia that is closer to Python, while both version can compile to the same machine instructions
    + the example(s) should be reasonably complicated
    + showing how to achieve performance with a simple example in python is on one hand quite a nice demonstration on the other hand it may not be that convincing, as I am not that fluent neither in Numba nor in Cython (it has not been built for that)
        * the choice for an example should rather show the limits of those optimizations, this however goes even deeper into the problem
        * should probably avoid matrix, linear algebra, as there is a lot to be done on the python side
        * do optimizations introduce additional complexity and hinder productivity

- teaching Julia vs convincing to use Julia vs showing what we like
    + it is hard to show its strong-points unless the audience knows something about the language or generally any other language
    + be upfront Julia is not for everyone and everything

- plotting the number of lines against speed gives a nice insight into why we use Julia - https://yakir12.github.io/whyjulia/#/1/4

- the design choices, which lead to Julia were caused by the technical constraints
    + little bit of history and background from 2009 (by Stefan Karpinski)
        * PyPy was pretty new: 1.0 was released in 2007 – it was the first version to be able to run any substantial Python apps and there were no plans at the time for supporting any of NumPy;
        * Cython was even newer: initial release was 2007;
        * Numba didn’t exist: initial release was in 2012.
    + this state kind of led to the development of Julia though the authors were more influence by Matlab, C, Ruby and Scheme
    + "Numerical computing is just not a priority for the Python core devs – and reasonably so, since that’s not the language’s primary focus."
    + fastest computation is the one that you don't do
    + Julia has never had a full interpreter, where the object and scopes are represented as dictionaries, as it is to slow for its purposes
    + the choice of technologies dictated features, that were implemented into the language
        * if something was hard to generate LLVM IR code for, it was not added
    + "People come for the speed but stay for the type-dispatch system."
    + Julia does not want to be magical black box, however the impression is not that easy to get rid of (personal experience)
    + JIT compilation is sometimes slow

- bring out the readability of code
    + anonymous functions, closures are the same (python uses lambda syntax for anonymous function and partial from some other pkg to make the closure)
    + you don't have to write nasty=optimized in order to run fast
        * close to mathematical representation
        * no need to write out for loops or fuse things unnaturally in order to make it faster (vectorization in MATLAB)
    + the dot syntax
        * for arithmetic operation but also for any generic function
        * intuitive broadcasting over tensors
    + no need to write functions with different names in order to differentiate the type of arguments it can take
    + no more digging around in C/Fortran as most of the base functionality is written in Julia
- interpolation is not just for strings but for any code/expression
```julia
    a = :(4+2)  # expression
    $a          # evaluation
```
    + shows a little bit of the meta-programming capabilities
- meta-programming
    + macros for different kind of things
        * @time for measuring time
        * @which to show which function will be call with current arguments
        * @macroexpand to show what the macro does with the code

- different kind of REPLs
    + `;` SOTA bash pipelining, which can transform Julia into a administrative scripting language with slightly beefier runtime
    + `]` to run pkg commands
    + `?` to run help with fuzzy search
    + additional REPLs such as R, C++ can be easily installed

- internal design of the language
    + allows for great interoperability of pkgs
    + how do we get from Julia to ASM
        * Parsing
        * Lowering
        * Type Inference
        * LLVM
        * ASM
    + what do macros do
    + generated functions

- type system
    + show the dual number example, where you can define forward automatic differentiation with less than 40 lines of code
    + user defined types are no more different from the built in, which allows for zero cost abstraction when dealing with
        * dual numbers (automatic differentiation)
        * specific numeric types like intervals or fixed point numbers
        * colors so that we can intuitively work with matrix of colors instead of matrix of bytes or floats
    + there is no way of enforcing that some functions are implemented for a given type, i.e. we cannot specify methods, that need to be implemented for an abstract type and thus for every other type down the inheritance line
        * this is usual in OO languages such as Python, C++ and Java
        * one one hand it is less restrictive and more extendable, on the other hand not having such enforcing power makes it harder to keep track of what needs to be implemented in order for the new type to work properly
        * example: CustomArray <: AbstractArray, i.e. when implementing CustomArray which inherits from AA, we need to implement the size and getindex methods, however there are more methods to implement in order to make broadcasting over that array

- what is the holy grail of programming (a little bit of theory)
    + allow for our code to work for multiple types of input
    + allow for our code to handle different classes of input differently
    + allow for extension for new types of inputs, that we have not specified
    + subclassing (OOP), multiple dispatch, ...
    + there is something called the expression problem
        * "The expression problem is a new name for an old problem.[2][3] The goal is to define a datatype by cases, where one can add new cases to the datatype and new functions over the datatype, without recompiling existing code, and while retaining static type safety (e.g., no casts)." - Philip Wadler

- multiple dispatch
    + methods can show all the method associated with a function name
    + instead of writing functions with different name, in Julia you can come up with the correct name and write functions for different arguments
        * example: instead of writing fabs for floats and abs for ints you write as many functions called abs as is needed, which gets specialized one called
    + "The key idea here is that multiple dispatch allows many different packages to implement the same interface, and so if you write code to that interface, you will automatically be "package-independent"."
        * example: in differential equations "solve(prob,alg)" is syntax which is "package-independent"
    + extending behavior made easier by using hierarchy and promotion mechanism
        * example: we don't have to define abs for every input type, as the only thing needed is how to convert those types to some that we already implemented
- Arrays
    + bounds checking by default, however can be turned of
    + when dealing with custom arrays there is @boundscheck macro, which marks a piece of code, that checks the bounds, subsequently this can be turned of from the point of view of the user by @inbounds macro
    + when @inbounds is used the user must make sure, that the bounds are not stepped over, otherwise Julia just accesses the part of memory and may even crash the program
        * there are performance gains for not checking bounds and sometimes they cause the last gap to bridge to get C speed
        * does not remove boundscheck when used in global scope!
    + looping over arrays can be sped up if Julia knows, that the first index is one (special iterator OneTo(size))
