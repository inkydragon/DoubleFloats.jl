# DoubleFloats.jl

### Math with 85+ accurate bits.
#### Extended precision float and complex types

----

[![Build Status](https://travis-ci.org/JuliaMath/DoubleFloats.jl.svg?branch=master)](https://travis-ci.org/JuliaMath/DoubleFloats.jl)&nbsp;&nbsp;&nbsp;[![Docs](https://img.shields.io/badge/docs-stable-blue.svg)](http://juliamath.github.io/DoubleFloats.jl/stable/)&nbsp;&nbsp;&nbsp;[![codecov](https://codecov.io/gh/JuliaMath/DoubleFloats.jl/branch/master/graph/badge.svg)](https://codecov.io/gh/JuliaMath/DoubleFloats.jl)

----

## Installation

```julia
pkg> add DoubleFloats
```
or
```julia
julia> using Pkg
julia> Pkg.add("DoubleFloats")
```


## More Performant Than BigFloat

Comparing Double64 and BigFloat after setting BigFloat precision to 106 bits.

| op   | speedup |
|:-----|--------:|
| +    |     11x |
| *    |     18x |
| \    |      7x |
| trig |   3x-6x |
 _these results are from BenchmarkTools, on one machine_


## Examples

### Double64, Double32, Double16
```julia
julia> using DoubleFloats

julia> dbl64 = sqrt(Double64(2)); 1 - dbl64 * inv(dbl64)
0.0
julia> dbl32 = sqrt(Double32(2)); 1 - dbl32 * inv(dbl32)
0.0
julia> dbl16 = sqrt(Double16(2)); 1 - dbl16 * inv(dbl16)
0.0

julia> typeof(ans) === Double16
true
```
note: floating-point constants must be used with care,
they are evaluated as Float64 values before additional processing
```julia
julia> Double64(0.2)
2.0000000000000001110223024625156540e-01

julia> Double64(2)/10
1.9999999999999999999999999999999937e-01

julia> d64"0.2"
1.9999999999999999999999999999999937e-01
```

### Complex functions
```julia

julia> x = ComplexD64(sqrt(d64"2"), cbrt(d64"3"))
1.4142135623730951 + 1.4422495703074083im

julia> y = acosh(x)
1.402873733241199 + 0.8555178360714634im

julia> x - cosh(y)
7.395570986446986e-32 + 0.0im
```
### show, string, parse
```julia
julia> using DoubleFloats

julia> x = sqrt(Double64(2)) / sqrt(Double64(6))
0.5773502691896257

julia> string(x)
"5.7735026918962576450914878050194151e-01"

julia> show(IOContext(Base.stdout,:compact=>false),x)
5.7735026918962576450914878050194151e-01

julia> showtyped(x)
Double64(0.5773502691896257, 3.3450280739356326e-17)

julia> showtyped(parse(Double64, stringtyped(x)))
Double64(0.5773502691896257, 3.3450280739356326e-17)

julia> Meta.parse(stringtyped(x))
:(Double64(0.5773502691896257, 3.3450280739356326e-17))

julia> x = ComplexD32(sqrt(d32"2"), cbrt(d32"3"))
1.4142135 + 1.4422495im

julia> string(x)
"1.414213562373094 + 1.442249570307406im"

julia> stringtyped(x)
"ComplexD32(Double32(1.4142135, 2.4203233e-8), Double32(1.4422495, 3.3793125e-8))"
```



## Accuracy


results for f(x), x in 0..1
 

| function |   abserr   |   relerr   |
|:--------:|:----------:|:----------:|
|   exp    |  1.0e-31   |   1.0e-31  |
|   log    |  1.0e-31   |   1.0e-31  |
|          |            |            |
|   sin    |  1.0e-31   |   1.0e-31  |
|   cos    |  1.0e-31   |   1.0e-31  |
|   tan    |  1.0e-31   |   1.0e-31  |
|          |            |            |
|  asin    |  1.0e-30   |   1.0e-30  |
|  acos    |  1.0e-30   |   1.0e-29  |
|  atan    |  1.0e-31   |   1.0e-30  |
|          |            |            |
|          |            |            |
|   sinh   |  1.0e-31   |   1.0e-29  |
|   cosh   |  1.0e-31   |   1.0e-31  |
|   tanh   |  1.0e-31   |   1.0e-29  |
|          |            |            |
|  asinh   |  1.0e-31   |   1.0e-29  |
|  atanh   |  1.0e-31   |   1.0e-30  |


results for f(x), x in 1..2
 

| function |   abserr   |   relerr   |   notes   |
|:--------:|:----------:|:----------:|:---------:|
|   exp    |  1.0e-30   |   1.0e-31  | |
|   log    |  1.0e-31   |   1.0e-31  | |
|          |            |            | |
|   sin    |  1.0e-31   |   1.0e-31  | |
|   cos    |  1.0e-31   |   1.0e-28  | |
|   tan    |  1.0e-24   |   1.0e-28  | near asymptote |
|          |            |            | |
|  asin    |  1.0e-30   |   1.0e-30  | |
|  acos    |  1.0e-30   |   1.0e-29  | |
|  atan    |  1.0e-31   |   1.0e-30  | |
|          |            |            | |
|          |            |            | |
|   sinh   |  1.0e-30   |   1.0e-31  | |
|   cosh   |  1.0e-30   |   1.0e-31  | |
|   tanh   |  1.0e-31   |   1.0e-31  | |
|          |            |            | |
|  asinh   |  1.0e-31   |   1.0e-31  | |


## Good Ways To Use This

In addition to simply `using DoubleFloats` and going from there, these two suggestions are easily managed
and will go a long way in increasing the robustness of the work and reliability in the computational results.   

If your input values are Float64s, map them to Double64s and proceed with your computation.  Then unmap your output values as Float64s, do additional work using those Float64s. With Float32 inputs, used Double32s similarly. Where throughput is important, and your algorithms are well-understood, this approach be used with the numerically sensitive parts of your computation only.  If you are doing that, be careful to map the inputs to those parts and unmap the outputs from those parts just as described above.


## Questions

Usage questions can be posted on the [Julia Discourse forum][discourse-tag-url].  Use the topic `Numerics` (a "Discipline") and a put the package name, DoubleFloats, in your question ("topic").

## Contributions

Contributions are very welcome, as are feature requests and suggestions. Please open an [issue][issues-url] if you encounter any problems. The [contributing page][contrib-url] has a few guidelines that should be followed when opening pull requests.

[contrib-url]: https://juliamath.github.io/DoubleFloats.jl/latest/man/contributing/
[discourse-tag-url]: https://discourse.julialang.org/tags/doublefloats
[gitter-url]: https://gitter.im/juliamath/users

[docs-current-img]: https://img.shields.io/badge/docs-latest-blue.svg
[docs-current-url]: https://juliamath.github.io/DoubleFloats.jl

[codecov-img]: https://codecov.io/gh/JuliaMath/DoubleFloats.jl/branch/master/graph/badge.svg
[codecov-url]: https://codecov.io/gh/JuliaMath/DoubleFloats.jl

[issues-url]: https://github.com/JuliaMath/DoubleFloats.jl/issues
