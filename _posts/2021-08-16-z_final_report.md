---
title: Final Report
layout: post
description: null
image: null
open_blog: true
suburl: "2021/08/16/z_final_report.html"
---

This report summarizes the work done in my GSoC 2021 project, **Supporting Arrays and Allocatables in LFortran** wth LFortran. A step by step development of the project is available at [czgdp1807.github.io](https://czgdp1807.github.io).

**About Me**

I am a final year Bachelor of Technology student at Indian Institute of Technology, Jodhpur in the department of Computer Science and Engineering.


**Project Outline**

This project aimed to add support for arrays and allocatables in LFortran.  There were some miscellaneous goals as well, such as improving support for pointers and kinds and some bug fixes discovered along the way. The original plan of the project is listed as follows,

1. **Community Bonding** - During the community bonding period, work on declaring arrays was supposed to be complete, and array initialisers in the phase of implementation. Moreover, operations on arrays were planned to be under discussions.
2. **Phase 1** - In this phase, features like operations on arrays were supposed to be added, along with indexing and slicing arrays, discussing ways to pass arrays as function/subroutine arguments.
3. **Phase 2** - In the final phase, I had planned to complete work on passing arrays as function/subroutine arguments, implementing intrinsic functions for arrays and adding support for allocatable arrays.

**Pull Requests**

This section describes the actual work done during the coding period in terms of merged PRs.

1. **Community Bonding**

- [Adding array intrinsic functions at LLVM level](https://gitlab.com/lfortran/lfortran/-/merge_requests/918)

- [Name Mangling and Corner Case checks](https://gitlab.com/lfortran/lfortran/-/merge_requests/930)

- [Completing basic array declaration](https://gitlab.com/lfortran/lfortran/-/merge_requests/931)

- [ArrayInitializer expressions with ImpliedDoLoops and Pass to DoLoop](https://gitlab.com/lfortran/lfortran/-/merge_requests/932)

2. **Phase 1**

- [Adding support for Array operation](https://gitlab.com/lfortran/lfortran/-/merge_requests/939)

- [Support for Array Slicing](https://gitlab.com/lfortran/lfortran/-/merge_requests/943)

- [Assinging non-ArrayInitializer expressions to all elements of an Array](https://gitlab.com/lfortran/lfortran/-/merge_requests/944)

- [Adding support for lbound and ubound](https://gitlab.com/lfortran/lfortran/-/merge_requests/946)

- [Passing Arrays to User defined functions](https://gitlab.com/lfortran/lfortran/-/merge_requests/947)

3. **Phase 2**

- [Support for Allocatables](https://gitlab.com/lfortran/lfortran/-/merge_requests/976)

- [Extending array_op.cpp for all operations](https://gitlab.com/lfortran/lfortran/-/merge_requests/998)

- [ImplicitDeallocate and ExplicitDeallocate](https://gitlab.com/lfortran/lfortran/-/merge_requests/1018)

- [Refactoring Array Descriptor Access](https://gitlab.com/lfortran/lfortran/-/merge_requests/1026)

- [Fixing for assinging arrays to arrays](https://gitlab.com/lfortran/lfortran/-/merge_requests/1054)

- [Associate Construct](https://gitlab.com/lfortran/lfortran/-/merge_requests/1097)

- [Allocatable strings](https://gitlab.com/lfortran/lfortran/-/merge_requests/1104)

**Future Work**

Future work for arrays include optimizations for array operations such as array tiling, trying out various descriptors. Following are the links to relevant issues,

- [LLVM: refactor array descriptor access](https://gitlab.com/lfortran/lfortran/-/issues/418) - See second point.

- [Loop tiling](https://gitlab.com/lfortran/lfortran/-/issues/428)

**Thoughts and Learnings**

A major point which I learnt during my project is that writing compilers requires designing algorithms along with paying attention to ease of use for the end user. To make that possible one needs to write code for several corner cases which we usually tend to ignore. For example, in LLVM, it is not possible to add an integer with a floating point number. A cast should be performed before performing the addition. In the following three points, I have shared some similar experiences, 

- **Array Operations** - We implemented this feature by converting statements like `c = a + b` to `do` loops with a body like, `c(i) = a(i) + b(i)`. Here, `c`, `a` and `b` are arrays. Now, this requires two things. First figuring out, where the result should go and then what's the starting and ending point of each dimension. For the second, Fortran provides `lbound` and `ubound` for arrays. We implemented them first and then this feature. For deciding the result variable, one may need to keep track of it during the conversion of array operations to loops. For example, in `c = a + b + d`. First, `a + b` will be converted to do loop and its result will be stored in a temporary variable, say `x`. Then, `c = x + d` will be converted to do loop and the result will be directly sent to `c`. This has to happen for any operation and any statement where such operations are present which makes it quite challenging. I implemented a recursive algorithm while keeping `result_var` as a global variable which tracks whether the result should go to a temporary variable or some variable already provided by the user. For example, once we go from current node, say, `Add(Add(a, b), d)` to `Add(a, b)`, we need to update the `result_var` from `c` to `x` (a newly created one). Once come back from `Add(a, b)` to `Add(Add(a, b), d)`, the reverse happens.

- **Returning Arrays from Functions** - The reason why I am mentioning about this feature is because of its elegant implementation. Literally returning arrays from functions may require creating a new array inside the function and then copying it to the destination once that array is returned. Say, for example, `d = f(a, b, c)`. `f` will first return an array say, `ret`, then this will be copied to `d`, resulting in doubling the peak memory consumption. However, if we convert `f` to a subroutine, then the previous call will become, `call f(a, b, c, d)`. Now, `f` will directly write to `d`. So, no extra memory will be required. Thanks to Ondrej for suggesting this approach.

- **Segmentation Faults and Double Free** - Ah! This was the most annoying part of my project. Espescially when I was implementing automatic deallocation of arrays on heap memory, I had to deal with a bunch of double free errors. Things got messier when an array got automatically freed before a subroutine call but inside the subroutine it wasn't again assigned some memory. This resulted in several segmentation faults one after the other and fixing them was no easy.

Overall, I think this project has made me a better programmer, problem solver and yeah a debugger (😏) too.
