---
title: Final Report
layout: post
description: null
image: null
open_blog: true
suburl: "2019/08/20/z_final_report.html"
---

This report summarizes the work done in my GSoC 2019 project, **Enhancement of Statistics Module** wth SymPy. A step by step development of the project is available at [czgdp1807.github.io](https://czgdp1807.github.io).

**About Me**

I am a third year Bachelor of Technology student at Indian Institute of Technology, Jodhpur in the department of Computer Science and Engineering.


**Project Outline**

The project plan was focused on the following areas of statistics that were required to be added to `sympy.stats`.

1. **Community Bonding** - I was supposed to add, Dirichlet Distribution, Multivariate Ewens Distribution, Multinomial Distribution, Negative multinomial distribution, and Generalized multivariate log-gamma distribution to `sympy.stats.joint_rv_types`.
2. **Phase 1** - I was supposed to work on stochastic processes, primraly on Markov chains, including it's API design, algorithm and implementation.
3. **Phase 2** - I was expected to work on random matrices, including Gaussian ensembles and matrices with random expressions as their elements.
4. **Phase 3** - I planned to work on assumptions of dependence, improving result generation by `sympy.stats` and improving other modules so that `sympy.stats` can function properly.

**Pull Requests**

This section describes the actual work done during the coding period in terms of merged PRs.

1. **Community Bonding**

- [#16576](https://github.com/sympy/sympy/pull/16576): This PR added `Dirichlet` and `MultivariteEwens` distributions.

- [#16808](https://github.com/sympy/sympy/pull/16808) : This PR added `Multinomial` and `NegativeMultinomial` distribution.

- [#16810](https://github.com/sympy/sympy/pull/16810) : This PR improved the API of `Sum` by allowing `Range` as the limits.

- [#16825](https://github.com/sympy/sympy/pull/16825) : This PR in continuation, added `GeneralizedMultivariateLogGamma` distribution. This was an interesting one due to the complexity involved in its PDF.

- [#16834](https://github.com/sympy/sympy/pull/16834) : This PR enhanced the `Multinomial` and `NegativeMultinomial` distributions by allowing symbolic dimensions for them.

2. **Phase 1**

- [#16897](https://github.com/sympy/sympy/pull/16897) : This was related to `sympy.core` and it helped in removing disparity in the results of special function `gamma`.

- [#16908](https://github.com/sympy/sympy/pull/16908) : This PR improved `sympy.stats.frv` by allowing conditions with foriegn symbols.

- [#16913](https://github.com/sympy/sympy/pull/16913) : This removed the unreachable code from `sympy.stats.frv`.

- [#16914](https://github.com/sympy/sympy/pull/16914) : This PR allowed symbolic dimensions to `MultivariateEwens` distribution.

- [#16929](https://github.com/sympy/sympy/pull/16929) : This one was for the `sympy.tensor` module. It optimized the `ArrayComprehension` and covered some corner cases.

- [#16981](https://github.com/sympy/sympy/pull/16981) : This PR added the architecture of stochastic processes. It also added discrete Markov chain to `sympy.stats`.

- [#17030](https://github.com/sympy/sympy/pull/17030) : Some features like, `joint_dsitribution` were added to stochastic processes in this PR.

- [#17046](https://github.com/sympy/sympy/pull/17046) : Some common properties of discrete Markov chains, like fundamental matrix, fixed row vector were added.

3. **Phase 2**

- [#16934](https://github.com/sympy/sympy/pull/16934) : The bug fixes for `sympy.stats.joint_rv_types` were complete and the further work has been handed over to my co-student, Ritesh.

- [#16962](https://github.com/sympy/sympy/pull/16962) : This was continuation of the work done in phase 1 for allowing symbolic dimensions in finite random variables. As I planned, this PR got merged in phase 2, after some changes.

- [#17083](https://github.com/sympy/sympy/pull/17083): The work done in this PR framed the platform and reason for the next one. The algorithm that got merged was a bit difficult to extend, and maintain. Thanks to Francesco for his [comment](https://github.com/sympy/sympy/pull/17083#issuecomment-508256359) for motivating me to re-think the whole framework.

- [#17163](https://github.com/sympy/sympy/pull/17163) : This was one of the most challenging PRs of the project, because, it involved re-designing the algorithm, refactoring the code and moreover lot of thinking. The details can be found at [this comment](https://github.com/sympy/sympy/pull/17163#issuecomment-510939984).

3. **Phase 3**

- [#17174](https://github.com/sympy/sympy/pull/17174) : In this PR, Gaussian ensembles were added to `sympy.stats`.

- [#17304](https://github.com/sympy/sympy/pull/17304) : While working on the above PR, I got an idea to open this one to add cicular ensembles to `sympy.stats`. I learned a lot about Haar measure while working.

- [#17306](https://github.com/sympy/sympy/pull/17306): This PR added matrices with random expressions. The challenging part of this PR was to generate canonical results for passing the tests.

- [#17336](https://github.com/sympy/sympy/pull/17336) : This was related to bug fix in `Q.ask` and `Matrix`. Take a look at an example [here](https://github.com/sympy/sympy/pull/17336#issue-304058013).

**Miscellaneous Work**

This section contains some of my PRs related to miscellanous issues like, workflow improvement, etc.

- [#16899](https://github.com/sympy/sympy/pull/16899) : This was a workflow related to PR to ignore the `.vscode` folder.

- [#17003](https://github.com/sympy/sympy/pull/17003) : This PR ignored the `__pycahce__` folder by adding it `.gitignore` file.

**Future Work**

The following PRs are open and are in their last stages for merging. Any interested student can take a look at them to extend my work in his/her GSoC project.

- [#17387](https://github.com/sympy/sympy/pull/17387) : This PR aims to add support for assumptions of dependence among random variables, like, `Covariance`, etc.

- [#17146](https://github.com/sympy/sympy/pull/17146) : This PR is in its last stages to fix and upgrade the `Range` set and we are finalizing few things, like changes in the output of `Range`. As planned I was successful at writing exhaustive and systematic tests.

Apart from the above, work on densities of Circular ensembles remains to be done. One can read the Theorem 3, page 8 of [this paper](https://arxiv.org/pdf/1103.3408.pdf).
