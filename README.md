# DoubleFloats.jl
### Floating point math with 100+ bit accurate significand; fast ops with 88+ bit accuracy.

## [Looking Ahead](https://github.com/JuliaMath/DoubleFloats.jl/blob/master/docs/src/lookingahead.md)


-----

| this package is under development |
|-----------------------------------|
| repository created on 2018-01-25  |


# DoubleFloats

*Floating point math with greater accuracy than Float32, Float64 types obtain."


| **Documentation**                                                               | **PackageEvaluator**                                                                            | **Build Status**                                                                                |
|:-------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------:|
| [![][docs-stable-img]][docs-stable-url] [![][docs-latest-img]][docs-latest-url] | [![][pkg-0.6-img]][pkg-0.6-url] [![][pkg-0.7-img]][pkg-0.7-url] | [![][travis-img]][travis-url] [![][appveyor-img]][appveyor-url] [![][codecov-img]][codecov-url] |


## Installation

The package is registered in `METADATA.jl` and can be installed with `Pkg.add`.

```julia
julia> Pkg.add("DoubleFloats")
```

## Documentation

- [**STABLE**][docs-stable-url] &mdash; **most recently tagged version of the documentation.**
- [**LATEST**][docs-latest-url] &mdash; *in-development version of the documentation.*

## Project Status

The package is tested against Julia `0.6` and *current* `0.7-dev` on Linux, OS X, and Windows.

## Questions and Contributions

Usage questions can be posted on the [Julia Discourse forum][discourse-tag-url] under the `doublefloats` tag, and/or in the [JuliaMath Gitter chat room][gitter-url].

Contributions are very welcome, as are feature requests and suggestions. Please open an [issue][issues-url] if you encounter any problems. The [contributing page][contrib-url] has a few guidelines that should be followed when opening pull requests and contributing code.

[contrib-url]: https://juliamath.github.io/DoubleFloats.jl/latest/man/contributing/
[discourse-tag-url]: https://discourse.julialang.org/tags/doublefloats
[gitter-url]: https://gitter.im/juliamath/users

[docs-latest-img]: https://img.shields.io/badge/docs-latest-blue.svg
[docs-latest-url]: https://juliamath.github.io/DoubleFloats.jl/latest

[docs-stable-img]: https://img.shields.io/badge/docs-stable-blue.svg
[docs-stable-url]: https://juliamath.github.io/DoubleFloats.jl/stable

[travis-img]: https://travis-ci.org/JuliaMath/DoubleFloats.jl.svg?branch=master
[travis-url]: https://travis-ci.org/JuliaMath/DoubleFloats.jl

[appveyor-img]: https://ci.appveyor.com/api/projects/status/xx7nimfpnl1r4gx0?svg=true
[appveyor-url]: https://ci.appveyor.com/project/JuliaMath/doublefloats-jl

[codecov-img]: https://codecov.io/gh/JuliaMath/DoubleFloats.jl/branch/master/graph/badge.svg
[codecov-url]: https://codecov.io/gh/JuliaMath/DoubleFloats.jl

[issues-url]: https://github.com/JuliaMath/DoubleFloats.jl/issues


[pkg-0.6-img]: http://pkg.julialang.org/badges/DoubleFloats_0.6.svg
[pkg-0.6-url]: http://pkg.julialang.org/?pkg=DoubleFloats&ver=0.6
[pkg-0.7-img]: http://pkg.julialang.org/badges/DoubleFloats_0.7.svg
[pkg-0.7-url]: http://pkg.julialang.org/?pkg=DoubleFloats&ver=0.7
