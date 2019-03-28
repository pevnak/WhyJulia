
# Type instability is sometimes just not well designed code
```julia
function return_if_even(a_number)
    if a_number % 2 == 0
        return a_number
    else
        return "This is not even!"
    end
end
```

# Defining structure with parameters, that acts like a function
- now implemented in ParametrizedFunctions.jl, handy when dealing with ODEs
```julia
struct  LotkaVolterra <: Function
         a::Float64
         b::Float64
end
f = LotkaVolterra(0.0,0.0)
(p::LotkaVolterra)(du,u,t) = begin
         du[1] = p.a * u[1] - p.b * u[1]*u[2]
         du[2] = -3 * u[2] + u[1]*u[2]
end
f([0.0, 0.0], [1.0, 2.0], 0.0)
```

# Combining containers of different shapes
- the idea of dimension for vectors is in the language and syntax
```julia
julia> rowvec = [1 2 3]
1×3 Array{Int64,2}:
 1  2  3

julia> colvec = [10,20,30]
3-element Array{Int64,1}:
 10
 20
 30

julia> rowvec .+ colvec
3×3 Array{Int64,2}:
 11  12  13
 21  22  23
 31  32  33
```