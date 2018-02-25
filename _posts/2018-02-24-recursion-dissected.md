---
layout: post
date: 2018-02-24 22:40
title:  "Recursion Dissected"
mood: happy
---

### Introduction
In this blog post I will try to give an intuition behind recursion and also discuss things that helped me understand the topic very well. Grasping recursion truly opens up solutions to many programming problems which otherwise would have to be coded with quite a bit of complexity.

### What is recursion?
Many programming text books define recursion as function that calls itself. Although the definition is sound but I feel it is incomplete and does not give you the intuition behind why and where recursion comes into play. I like to think of recursion as technique in which you break down a problem into smaller subproblems and then combine the solution of smaller problem to deduce the final solution you need. There is a lot of intuition behind recursion if you compare it to **Principle of Mathematical Induction (PMI)**. PMI is a technique used to prove theorems or a formula. There are typically 3 steps involved in PMI. Lets try to prove sum of n integers Sum(n) = n(n+1)/2
* Base case  
  Assume the formula or theorem is true for n=1
  Therefore sum(1) = 1(1+1)/2 = 2/2 = 1
* Induction hypothesis  
  Assume sum(n) = n(n+1)/2 is true for some n
* Prove that the theorem is true for n+1 using steps 1 and 2  
  Sum(n+1) = (n+1) ((n+1)+1)/2
  1+2+3+...+n+1 = (n+1)((n+1)+1)/2
  LHS can be written as
  n(n+1)/2 + n+1 = (n+1)(n+2)/2
  factoring out n+1 we get
  (n+1)(n+2)/2 which is equal to RHS
