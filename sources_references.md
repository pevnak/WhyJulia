# Interesting videos
- John Pearson | Introduction to Julia for Pythonistas
    + https://youtu.be/Cj6bjqS5otM
    + uses Julia 0.5, but quite a lot of still valid points there
- Keno Fischer | The Julia Language and C++: The Perfect Marriage?
    + https://youtu.be/hvnxY3NjHQ4?t=2580
    + amazing talk about fusing C++ with Julia to achieve greatness
- Jeff Bezanson | Why is Julia fast?
    + https://www.youtube.com/watch?v=cjzcYM9YhwA
    + why are we not hitting the theoretical performance
    + the cause - uncertainty
    + system language/scripting language
    + "everything as a pointer is wrong approach"
    + dynamic glue around fast kernels
        * the two language problem causes headache as you always have to think about which parts to write in C and how to correctly interface with the rest
- George Datseris | Why Julia is the most suitable language for science 
    + https://youtu.be/7y-ahkUsIrY
    + points out 
        * custom infix operators for example in use with tensor product 
        * assignments return values
    + includes small JuliaDynamics presentation
    + shows another case where MD is better than OOD (collision time)
    + 16:26 - 1 to 1 representation of algorithm for Ljapunov exponent computation

# Interesting articles
- Christopher Rackauckas | Some State of the Art Packages in Julia v1.0
    + http://www.stochasticlifestyle.com/some-state-of-the-art-packages-in-julia-v1-0/
    + picks some of the prime jewels of the Julia Pkg ecosystem
- Josh Day | Why I use Julia
    + https://www.seqstat.com/post/whyjulia/
- Erik Engheim | Defining Custom Units in Julia and Python
    + https://medium.com/@Jernfrost/defining-custom-units-in-julia-and-python-513c34a4c971
    + defining types for different temperature scales
    + interesting programming patter, that is hard to design in Python but easy and readable in Julia
- Kevin Modzelewski | Personal Thought about Pyston Outcome
    + http://blog.kevmod.com/2017/02/personal-thoughts-about-pystons-outcome/
    + Pyston = JIT compiler for Python
    + pythons performance struggles are in part due to its object design, that allows to override almost everything everywhere during runtime and its used extensively
    + the compiler thus can assume only so little
- Simon Danisch | The Julia Language Challenge
    + https://nextjournal.com/sdanisch/the-julia-challenge
    + "I've been using the Julia language for around 5 years now, and I've grown rather fond of it. By now, I can't really imagine how to do the things I'm doing in any other language. This could, of course, be a misconception and the result of not knowing any other language well enough - a form of the Dunning–Kruger effect. But my impression is that Julia is the best language to write high performance numeric libraries for machine learning, data science, solvers, optimizations, etc...."
    + challenges other programmers with different language background to implement broadcasting in their own languages
- Steve G. Johnson, Matt Bauman | Dot syntax articles
    + https://julialang.org/blog/2017/01/moredots
    + https://julialang.org/blog/2018/05/extensible-broadcast-fusion
    + power of dot syntax is in my opinion quite unique and needs to be put forward
    + reworks in 0.7 - broadcasting is first class data structure and makes even more flexible

# Interesting discussions
- Not only for technical computing: changing the narrative ...
    + https://discourse.julialang.org/t/not-only-for-technical-computing-changing-the-narrative-around-the-usecase-for-julia/19784
- Comparing Python, Julia and C++
    + https://discourse.julialang.org/t/comparing-python-julia-and-c/17019
    + shows how difficult is to show performance difference, when you are not fluent in every language
    + also the importance of a good example to test on (Julia does sometimes unintuitive things)
- Julia motivation: why weren't Numpy, SciPy, Numba good enough?
    + https://discourse.julialang.org/t/julia-motivation-why-werent-numpy-scipy-numba-good-enough/2236
    + old time favorite discussion
    + pkg synergies, that just work out of the box, without glue code
        * example: Measurements.jl
- How hard would it be to implement Numpy.jl
    + https://discourse.julialang.org/t/how-hard-would-it-be-to-implement-numpy-jl-i-e-numpy-in-julia/22080/56
    + kind of dead end discussion about a project that makes very little sense with person that might be a little stubborn
    + one has to be prepared for this, stevengj could not really control himself and suggested the OP to rather use Fortran 77...
- Preaching Julia to biologist
    + https://discourse.julialang.org/t/preaching-julia-to-biologists/15058/75
    + how to approach the topic of Julia adoption
    + one thing that stood out here is that we should probably talk about what we have found nice about the language and not try to primarily convert other people to it

# Other interesting sources
- John Gibson | Why Julia?
    + https://github.com/johnfgibson/whyjulia
    + nicely divided presentation with actual examples of Julia in practice

- Chris Rackauckas | Why Julia?
    + http://ucidatascienceinitiative.github.io/IntroToJulia/Html/WhyJulia
    + "Julia essentially answers the Pyston question: how should a language be restricted and thought about so that way it still looks and acts dynamic, but in the end is very easy to extend and optimize? When you understand how Julia’s type system allows for JIT compilation to not just work, but work very well by specializing on exactly the functions its seeing, then you see what makes Julia special and how to apply this design to your own codes to get similar results."

- JuliaComputing | Julia Tutorials
    + https://github.com/JuliaComputing/JuliaBoxTutorials
    + tutorials, that are available on JuliaBox