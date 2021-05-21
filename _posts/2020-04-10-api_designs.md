---
title: Designing APIs
layout: post
description: null
image: null
open_blog: true
suburl: "2020/04/10/api_designs.html"
---

It's been quite some time, around 2 years or so, I have been contributing to various projects on Github and majority of my time goes into discussions, rather than coding things out. It was in the summers of 2019 when I started to write code from scratch rather than fixing bugs in others' codes. I was supposed to write code for Markov chains, as a part of GSoC with SymPy. Well, I literally coded it out without even discussing about it's design with the community and as expected my patch was rejected for a first few times. Thanks to Francesco who told me about my mistake that we shouldn't just dive into implementation when writing quality software which is to be used by a lot of users and not just me. He told that the first step of a software engineering pipeline is designing **stable** APIs through some use cases. So, in this blog, I will share with you my thoughts, on the basis of my experiences, on how to design APIs, on what parameters an API should be judged.

For those who do not know, an API is something like a function prototype in C++ i.e., what arguments do you need to call a function and in what order they should be passed to a function. For example, `bool search(std::vector<int>& v, int x)` is an API to search for an element `x` in a C++ vector which returns a `bool` value. That's all you need to know for now.

Now, let's come to the question of how to approach the problem for designing APIs. Let's take an example, of sorting, for now in ascending order, elements in place in a container. The first step is to take a simple use case(or we say, example) of this problem. I have C++ `std::vector<int> u = {3, 1, 2}` and it should be sorted as said above. So a prototype of a function doing this task can look like as follows,

```cpp
sort(std::vector<int>& v);
```

I would be required to make a call like, `sort(u)` and my vector will be sorted. However, what if I want to sort my `vector` in descending order. Well, a simple solution would be provide an option like `desc` which should be `false` by default and if set to `true` will sort the array in descending order. So our API will change as follows,

```cpp
sort(std::vector<int>& v, bool desc=false);
```

So, for sorting in descending order I will be required to call `sort` as `sort(u, true)`. Note that `sort(u)` will still work as by default `desc` is `false`. Looks cool right? But, what if the elements are not at all integers, floats or something for which the built-in relational operators don't work. A vector with elements which are references to the instances of the following `struct`,

```cpp
struct Node
{
    int key, data;
};
```

A simple solution to this problem is to provide an option of custom comparators(if you have used `std::sort` then you might be aware about comparators.). If nothing is provided as comparator then they can default to `<=` operators.

```cpp
bool comp(Node& a, Node& b)
{
    return a.key <= b.key;
}
```

Now, our sort prototype looks like,

```cpp
sort(std::vector<Node&>& v, bool (*comp)(Node&, Node&)=ascending);
```

But wait now `sort` is overloaded a separate prototype for `int` and a separate prototype for `Node`. We cannot keept writing prototypes for each data type. What should we do? Well, we can use templates.

```cpp
template <class type>
sort(std::vector<type>& v, bool (*comp)(type&, type&)=ascending);
```

You might have noticed that there is no scope of sorting the vector from one index to another leaving the rest of the vector untouched. In fact, the above API doesn't even support anything other than vectors. So, now if we just include the above sort function in our project and in future if we want to support sorting for arrays then probably we can do it by overloading but if want to support sorting from one index to another, it will cause a blunder as code written using your package will fail and you do not want that.  If you want to see a real life example, just search about the API deprecation that happened when Tensorflow 2.x series was released.

Therefore the take away from the discussion till now is that we should design APIs by first taking some simple use cases and then improving upon your initial design by taking a lot more examples which usually happens in open source when several people from the community participate in discussions and give counter cases for your design. The end result is an API which can remain stable between successive realeses of the package you are working on.

Now, let's see how an API can be judged. I have listed some parameters below, which can help in deciding the same,

1. Unambiguity - This parameter can be explained through a simple example in Python where ambiguity can creep in very easily as it is a dynamically typed language. Let's say you want to sample some elements following Normal distribution using some external libraries, say, `numpy`, and `tensorflow`. It's quite possible that all of these aren't installed in a system, so you just check which one is installed and return the result using that library. Your API looks as follows,

```python
sample(distribution, size)
```

Clearly, we do not take library as the option and say, you first check if `numpy` is installed, if it is then you return a `numpy.array` object. If it isn't you go for `tensorflow` and if it is installed then you return `tf.Tensor` object. So, the user simply doesn't know what will be the type of the object while using your function. Ambiguity has creeped in and now the user has to check the type of the result before using it correctly. However, `sample` can be made unambiguous if we allow, `library` as an option and if a particular library isn't installed an error would be raised requesting the user to install the library before moving on. Corrective solution can be as follows,

```python
sample(distribution, size, library)
```

2. Consistency - Here we can consider an example which I came across while working on one of my data structures project. Say, there is a class called, `Deque` which is abstract and it has a method, `popleft`. A child class `ArrayDeque` implements `pop_left` and not `popleft`. So now if someone familiar with the interface of `Deque` will try to use `popleft` and will face an `NotImplementedError` as the class `Deque` is abstract. This is where consistency is important. If the interface class has `popleft` as an abstract method then in all the implementation classes `popleft` should be defined and any new method doing the same thing shouldn't be defined.

3. Non-redundant - This can be explained with an example of trinomial coefficients. Say you have function, `trinomial(n, k1, k2, k3)`. As it is a fact that, `n = k1 + k2 + k3`, so if the user wants to compute the result for `k1 = 1`, `k2 = 3`, `k3 = 4` then he/she will be unnecessarily required to pass, `n = 8` which causes the API to be redundant. In fact, this API will involve an extra check of the above constraint which will not be required if we do, `trinomial(k1, k2, k3)`.

4. Avoid too many options - Too many default options shouldn't be there in the API. Otherwise it will just make things hard to remember. I'd suggest to avoid default arguments wherever possible. You can take a look at [sympy.solve](https://docs.sympy.org/latest/modules/solvers/solvers.html#sympy.solvers.solvers.solve) and as you might have observed it has too many flags. A cleaner API, `solveset` is on it's way to replace `solve` just because of this dirty API.

At last I'd say just follow the KISS principle, i.e., **K**eep **I**t **S**imple **S**tupid.


