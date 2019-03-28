https://discourse.julialang.org/t/julia-motivation-why-werent-numpy-scipy-numba-good-enough/2236/3?u=janfrancu
Sure you can make Python fast in some cases where you use a small subset of the language. However, Python as a whole is extremely difficult to make fast because of the incredible freedom you have. The “compiler” can assume very little, so it is difficult to generate efficient code. Just consider the incredible amount of time and money that has been spent on trying to make it faster and the relatively mediocre success it has had (Pyston, Numba, PyPy etc).

jakevdp | Why Python is Slow: Looking Under the Hood
https://jakevdp.github.io/blog/2014/05/09/why-python-is-slow/

- Jean Francois Puget | How to make Python run as fast as Julia
    + https://www.ibm.com/developerworks/community/blogs/jfp/entry/Python_Meets_Julia_Micro_Performance?lang=en
    + the author goes to great lengths how to make the code faster
    + Fibonachi example:
        * Cython, typed Cython, caching computation (can be also done in Julia using Memoize pkg)
        * at the end dissolves recursion altogether making it really fast when using Cython or Numba, but kinda defeats the purpose of recursion test 
        * warning about installation difficulties with Cython, Numba  
    + "Installing Numpy can take a while, I recommend you use Anaconda or a Docker image where the Python scientific stack is already installed."
    + QuickSort example:
        * boils down to just use the built-in sorting algorithm
    + Mandelbrot example:
        * in subsequent article goes even further and implements it using gpus, but at that point the author does not compare the two completely different worlds
    + Vectorization:
        * in python one can vectorize an operation using ```vf = np.vectorize(`f)```
    + "Anyway, it is fair to say that on the micro benchmark, Python performance matches Julia performance when the right tools are used.  Conversely, we can also say that Julia's performance matches that of compiled Python.  This in itself is interesting given Julia does it without any need to annotate or modify the code."

- Jean Francois Puget | A speed comparison of C, Julia, Python, Numba and Cython on LU factorization
    + https://www.ibm.com/developerworks/community/blogs/jfp/entry/A_Comparison_Of_C_Julia_Python_Numba_Cython_Scipy_and_BLAS_on_LU_Factorization?lang=en
    + one can get to C speed with python, however there are many ways to get there and we don't know at the beginning, which one is the best
    + 2D indexing of C arrays, nice
    ```c
    inline int _(int row, int col, int rows){
        return row*rows + col;
    }
    ```

# Notes
- Numba is an auto-accelerating engine not just a compiler












