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
Now that we have a refresher on PMI lets look at how we can apply this in our recursive problem solving thinking.

### Recursive thinking
In this section we build up some techniques that once mastered can be utilized as templates for solving many recursive problems. One common mistake I see people make is to try to visualize and think through how recursive calls will work. This is ok when the problem domain is small but for complex problems this can get tedious and unreasonable. In some ways we have to assume that the solutions for smaller subproblems will work and are correct and all we have to do is apply or combine the smaller solutions to build the complete solution. This is very much like Induction hypothesis where we assume that proof is true for some n and have to prove it is true for n+1. This is what many people call **_Recursive leap of faith_**. Lets look at what I mean by **_Recursive leap of faith_** with an example. Suppose you are in group of 500 people standing right next to each other. The goal of this group is to figure out total salary of the entire group. Imagine that you are the last person in the group. If I told you that the person besides you will accurately tell you the sum of salaries for all other 499 people then your problem becomes relatively simple. All you will have to do is add your own salary + sumOfSalaries(499 other people) and you are done. Here you believed that the number returned by the person on your right is correct and you did not look into how it was calculated. Your task was pretty simple add your own salary to this number and pass it to the person next to you. Here you took **_Recursive leap of faith_** and believed in the process to work itself out. 
{: .text-justify}
