---
title: Community Bonding - A head start
layout: post
description: null
image: null
open_blog: true
suburl: "2019/05/27/bonding_period.html"
---

So, here I am with another set of experiences to share with you, i.e., the Community Bonding of GSoC. After discussing with my fellow developers, and my mentors, we reframed our timeline. I will be working on very interesting topics in statistics, including, joint distributions, Markov chains, random matrices, assumptions of dependence and simplifying the results of the stats module.

For a head start, I started working on adding multivariate distributions and the good news is that I have completed majority of the work, apart from some technical constraints which will be solved by another project very soon. If you are interested in seeing the code, take a look at the PRs [#16576](https://github.com/sympy/sympy/pull/16576), [#16808](https://github.com/sympy/sympy/pull/16808), [#16825](https://github.com/sympy/sympy/pull/16825). Infact, apart from the stats module, I also had an opportunity to work on other modules of SymPy, like, I improved the API of `Sum` in `sympy.concrete`, allowing `Range` to be passed as limits and that too while working on discrete joint distributions. You can check the PR [#16810](https://github.com/sympy/sympy/pull/16810) for the details. Thanks to [Christopher Smith](https://github.com/smichr) for helping me with this. Still there are issues like, [#16833](https://github.com/sympy/sympy/issues/16833) which require a lot of discussion before concrete implementation, will update you on this if some progress takes place.

Apart from coding, we had discussions on design of Markov chain and random matrices. I also made two prototypes at PR [#16852](https://github.com/sympy/sympy/pull/16852), and [#16866](https://github.com/sympy/sympy/pull/16866) . We are currently having more to think on this part, like API, class structure, etc.

Overall, the bonding period was very a great learning experience about how various modules affect each other and bring the best out of SymPy. See you soon in the next blog. :)