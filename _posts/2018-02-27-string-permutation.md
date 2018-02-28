---
layout: post
date: 2018-02-27 20:17
title:  "String Permutation"
mood: happy
---

#### Problem Statement
The problem we are going to formalute a solution is as follows  
Given a string of of size 'n' find all permutations of the string.  
So if given string is "abc" the answer will be {'abc','acb','bac','bca','cab','cba'}. This problem has a very elegant solution if expressed via recursion. Let us try to build our intuition for this problem first before we write any code. We will look at string "abc" and try to break down the problem in recursive template.  
permutation("abc") can be broken down into one set of subproblem  such as 
a + permutation("bc"). Suppose I told you that the permutation("bc") will be provided to you, then your problem will be simple as prepending 'a' to the strings in result set. It will look something like this  
permutation("bc") --> ["bc", "cb"] and now we prepend 'a' to these individual strings to get the following set ["abc", "acb"]. This provides us the partial subset of our answer. Similarly we will have to do this for every character in the string. See below
```
b + permutation("ac")
b + ["ac", "ca"]
["bac", "bca"]
```

```
c + permutation("ab")
c + ["ab", "ba"]
["cab", "cba"]
```
There is pattern that we can present with an equation --  
permutation(string) --> for every character in string  
                           do :
                               prepend current char + permutation(string without current char)  
                         
                         
There is one thing missing in our recursive strategy and that is the base case. The base case in our problem will be when the string is of size 0 we return. The code of this problem becomes very simple  
{% highlight java  %}
public class PermuteString {

  public static void permute(String orginal) {
    permute("", orginal);
  }
  
  public static void permute(String current, String remaining) {
    if(remaining.isEmpty()) {
      System.out.println(current);
      return;
    }
    
    //Go through each character in string and perform this  
    // current char + permutation(remaining string)  
    // remaining string -- the original string minus the currently selected  
    //character
    for(int i=0; i < remaining.length(); i++) {
      char c = remaining.charAt(i);
        
      permute(c+current, remaining.substring(0,i) + remaining.substring(i+1));
    }
  }

  public static void main(String[] args) {
    permute("abc");
  }
}
{% endhighlight %} 
