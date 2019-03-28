# What does science need from code?
source: 
    George Datseris | Why Julia is the most suitable language for science
    Nick Eubank | What Julia Offers Academic Researchers

## Steps
1. Figure out how the computer and language can help answer my question.
2. Realize and implement the idea in code.
3. Run the code.
4. Fetch results, visualize, debug.
5. Release

## Our needs
1. Solving the problem, i.e. the language has to allow you to solve it.
    + We would like to solve it quickly from the point of view of design and implementation.
    + "Performance of doing the science."
2. Speed in the computation phase, as it is the thing that will run many times.
3. Concise, intuitive, easy to read code.
    + Don't be afraid to show the code.
4. Code that is easy to share, install, use and replicate.
    + I would also add easy to extend.
5. Free and open source

## Nice to have in Base
- number types and their hierarchy
- extensive LinearAlgebra
- native parallelism

## Nice to have in general
- zero overhead units using Unitful
    + see potential of plotting the result, where on each axis there is also the unit defined, as there is metadata along the real data


## Case studies
### Differential equations
source:
    http://www.stochasticlifestyle.com/category/math/differential-equations/
    Confederated Modular Differential Equation APIs for Accelerated
Algorithm Development and Benchmarking
- SOTA pkg for solving PDE, ODE, 
- modular in its design
    + defined in one meta-package
    + solve method is the core of the design
        * input: problem, solver, args, kwargs
        * dispatched based on the given problem
        * output is standardized with common access methods
    + solver can be defined in its own pkg
- type hierarchy plus some heuristics allow for automatic specialization of solver for a given problem and solution requirements
- 

