---
layout: post
date: 2018-02-27 20:17
title:  "Letter Combinations of a Phone Number"
mood: happy
category: 
- string enumeration
- recursion
tags:
- recursion
- algorithms
- programming
---

#### Problem Statement
Given a string containing numbers from 2-9 enumerate all possible combinations that the number could represent. Each number is mapped to 3 or 4 digit code as shown in the image below. 
<figure>
    <img src="https://s3.amazonaws.com/amitchavan/blog/phone_number/digits.png"/>
</figure>

For example
 
```
Input:"23"
Output:["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

If we assume that every number has 3 character long code then the number of possible combinations for string of length n will be 3^n. Example above a string of length 2 you will get 3^2 possible combinations. This problem is really extension of String permutation about which I wrote in previous blog. Below is source code for solving the problem using recursion.
{% highlight java%}
public class PhoneNumberDigits {

  public static Map<Character, String> lookup = new HashMap<>();

  static {
    lookup.put('2', "abc");
    lookup.put('3', "def");
    lookup.put('4', "ghi");
    lookup.put('5', "jkl");
    lookup.put('6', "mno");
    lookup.put('7', "pqrs");
    lookup.put('8', "tuv");
    lookup.put('9', "wxyz");
  }

  public static List<String> enumerate(String digits) {
    List<String> results = new ArrayList<>();
    enumerate("", digits, results);
    return results;
  }

  private static void enumerate(String prefix, String digits, List<String> results) {
    if (!digits.isEmpty()) {
      char currentChar = digits.charAt(0);
      String charCode = lookup.get(currentChar);
      for (int i = 0; i < charCode.length(); i++) {
        enumerate(prefix + charCode.charAt(i), digits.substring(1), results);
      }
    } else {
      results.add(prefix);
      return;
    }
  }
}
{% end highlight%}