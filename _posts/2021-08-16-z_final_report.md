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
