---
title: Week 1 - All about design, imporvements and bug fixes
layout: post
description: null
image: null
open_blog: true
suburl: "2019/06/02/first_week.html"
---

The first week of official coding phase is over and it's time to tell you about what I did and what I learnt. So here it goes.

I started discussion with my mentor about API design of Markov chain. We have more clarity about the same than before. The final API will be somewhat closer to the one mentioned in [this](https://github.com/sympy/sympy/issues/16895#issuecomment-497649797) comment. The discussion about probability space of stochastic process is under way. We will conclude that soon.

I also made some PRs during this week for improving the distributions which I added during the bonding period. The PR [#16914](https://github.com/sympy/sympy/pull/16914) allowed the possibility of symbolic dimensions in `MultivariateEwens`. We earlier decided that we will use `ArrayComprehension` which one of my fellow students developed. However, currently it needs a lot of improvements before being put to use. I have made an attempt to optimise the code of `ArrayComprehension` via PR [#16929](https://github.com/sympy/sympy/pull/16929). It also covers some cases which were left during the inital merge. I have also tried to allow symbolic conditions to finite probability spaces. I have two approaches for review. One of them is in the [diff of PR #16908](https://github.com/sympy/sympy/pull/16908/files) and the other one is in [this](https://github.com/sympy/sympy/pull/16908#issuecomment-497950242) comment. I have also made some minor improvements like changing namespace of `joint_rv_types` via PR [#16919](https://github.com/sympy/sympy/pull/16919), enhancement of `P` in PR [#16907](https://github.com/sympy/sympy/pull/16907) and some general bug fixes in `MarginalDistribution` at PR [#16934](https://github.com/sympy/sympy/pull/16934).

Doing all this I learnt a lot of things. The most important was that API design matters the most. Without it, it's not possible to develop a good class structure. Thanks to Francesco for making me learn this fact. The other thing is, how sometimes even to make small changes in a large code base, it takes hours to get it right. Another fact which I learnt is how small optimisations in a large of code base can improve the performance.

See you next week with some more progress. :)