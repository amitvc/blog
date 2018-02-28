---
layout: post
date: 2018-02-24 22:40
title:  "Recursion Dissected"
mood: happy
category: 
- algorithms
- recursion
tags:
- recursion
- algorithms
- programming
---

### Introduction
In this blog post I will try to give an intuition behind recursion and also discuss things that helped me understand the topic very well. Grasping recursion truly opens up solutions to many programming problems which otherwise would have to be coded with quite a bit of complexity.

### What is recursion?
Many programming text books define recursion as a function that calls itself. Although the definition is sound, I feel it is incomplete and does not give you the intuition behind why and where recursion comes into play. I like to think of recursion as a technique in which you break down a problem into smaller subproblems and then combine the solution of a smaller problem to deduce the final solution you need. There is a lot of intuition behind recursion if you compare it to **Principle of Mathematical Induction (PMI)**. PMI is a technique used to prove theorems or a formula. There are typically 3 steps involved in PMI. Lets try to prove a sum of n integers Sum(n) = n(n+1)/2
* Base case  
  Prove the formula or theorem is true for small n. In this case n=1
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
In this section we build up some techniques that, once mastered, can be utilized as templates for solving many recursive problems. One common mistake I see people make is to try to visualize and think through how recursive calls will work. This is ok when a problem domain is small but for complex problems this can get tedious and unreasonable. In some ways we have to assume that the solutions for smaller subproblems will work and are correct and all we have to do is apply or combine the smaller solutions to build the complete solution. This is very much like Induction hypothesis, where we assume that proof is true for some n and have to prove it is true for n+1. This is what many people call **_Recursive leap of faith_**. Lets look at what I mean by **_Recursive leap of faith_** with an example. Suppose you are in a group of 500 people standing right next to each other. The goal of this group is to figure out a total salary of the entire group. Imagine that you are the last person in the group. If I told you that a person beside you will accurately tell you the sum of salaries for all other 499 people then your problem becomes relatively simple. All you will have to do is add your own salary + sumOfSalaries(499 other people) and you are done. Here you believed that the number returned by the person on your right is correct and you did not look into how it was calculated. Your task was pretty simple, add your own salary to this number and pass it to the person next to you. Here you took **_Recursive leap of faith_** and believed in the process to work itself out. Thus we broke down the problem into smaller subproblems and believed in the recursive process to work itself out. Of course there are few more things we will need to address such as base case, etc but at this point you understand what I mean by breaking down the problem and trusting that recursion will work itself out. The person at the 499 position did exactly the same; he added his own salary to sumOfSalaries(498 other people) and returned the value to you. Let's see how the pseudo code would look like
{% highlight java linenos %}
   int sumOfSalaries(int currentIndex, int n, int salaries[]) {  
      if(currentIndex == 0){  
        return salaries[currentIndex];  
      }  
    return salaries[currentIndex] + sumOfSalaries(currentIndex--, n, salaries);  
 }
 
 int aggregateSalary = sumOfSalaries(500-1, 500, salaries);
 /* Where salaries is an array that contains salary of all  
   500 ppl.n is total number of people  
   */
{% endhighlight %} 
If you look at the code above you will see at line 5 you add your own salary to the aggregate salaries of all prior. The base case is when you are the first person in the line. In that case we treat the problem as just returning the current salary.  
Lets look at another tricky problem that has an elegant recursive solution.
Invert a binary tree:  
Given a binary tree, our goal is to invert it. See the image below  
<figure>
    <img src="https://s3.amazonaws.com/amitchavan/blog/recursion/InvertTree.jpeg"/>
</figure>
Lets put on our recursive thinking hat and break down the problem. First at any given node we expect the right and left subtree below the node have already been inverted. Once that has happened our task is simply to replace the current nodes left subtree with the current nodes right subtree and vice-versa. So we take a **_Recursive leap of faith_** in assuming that our left and right child subtrees have already been reverted and now our current task only has to swap the left and right child. 
Lets see how we express this in pseudo code. 
```
   invert(node n) {
       if n is null return
       invert(left child of n)
       invert(right child of n)
       swap left and right child of n.
   }
```  
It turns out using recursion the solution to this problem turns out to be very compact code and very natural to express in terms of recursive strategy. See code below  
{% highlight java  %}
   public class InvertBinaryTree {
  
  public static class Node {
    public Node left, right;
    public int val;
    public Node(int v) {
      this.val = v;
    }
  }
  
  public static void invert(Node n) {
    if(n == null) {
      return;
    }
    //Invert my left subtree first
    invert(n.left);
    // Then invert my right subtree
    invert(n.right);
    //If i come here it means my left and right child subtrees 
    //are already inverted and now
    // my task is to simply swap my children 
    Node temp = n.left;
    n.left = n.right;
    n.right = temp;
  }

  public static void main(String[] args) {
    Node n20  = new Node(20);
    Node n35 = new Node(35);
    Node n15 = new Node(15);
    Node n10 = new Node(10);
    Node n18 = new Node(18);
    Node n40 = new Node(40);
    
    n20.left = n15;
    n20.right = n35;
    n15.left = n10;
    n15.right = n18;
    n35.right = n40;
    invert(n20);
  }
}
{% endhighlight %}

#### Good resources  
* https://www.codingninjas.in
* https://www.amazon.com/Introduction-Recursive-Programming-Manuel-Rubio-Sanchez/dp/1498735282

{: .text-justify}
