---
title: "POD #4 – Apples and Oranges"
date: 2025-10-01 10:00
categories: [Tech, Coding]
tags: [algorithm]
---

Today’s problem is one of those that looks very simple, yet you’ll probably spend more time understanding the statement than writing the actual solution. The nice touch is that it comes with apples and oranges, in case you’ve missed those primary school math exercises with fruits.

## Problem Statement

Sam’s house has an apple tree and an orange tree that yield an abundance of fruit.  
- `s`: starting point of Sam’s house location  
- `t`: ending point of Sam’s house location  
- `a`: location of the Apple tree  
- `b`: location of the Orange tree  
- `apples`: distances at which each apple falls from the tree  
- `oranges`: distances at which each orange falls from the tree  

The task is to print two numbers:  
1. The number of apples that fall on Sam’s house.  
2. The number of oranges that fall on Sam’s house.  


## Try it yourself first

If you have 10 minutes to spare and want a warm-up puzzle, I highly recommend solving it directly on [HackerRank](https://www.hackerrank.com/challenges/apple-and-orange/problem) before checking my solution. Don’t rush to the code and don’t use AI straight away. Try to reason it out yourself first. It’s a very simple, yet instructive problem.  


## My Approach

Once you understand how apples and oranges land on the number line, the solution is straightforward:  

- each fruit has a final position:  
  - `a + d` for apples  
  - `b + d` for oranges  
- check whether that position is in the interval `[s, t]`  
- count how many fall inside the range  

### Code (C#)

```csharp
public static void countApplesAndOranges(int s, int t, int a, int b, List<int> apples, List<int> oranges)
{        
    var houseApples = apples.Count(apple => s <= apple + a && apple + a <= t);
    var houseOranges = oranges.Count(orange => s <= orange + b && orange + b <= t);
    
    Console.WriteLine(houseApples);
    Console.WriteLine(houseOranges);
}
```
### Notes

- Time complexity: **O(m + n)**, where `m` is the number of apples and `n` the number of oranges.
- The code is compact, expressive, and easy to read.
- LINQ makes the counting very clean, avoiding unnecessary loops.

> Problems like this may look simple, but they’re perfect as small morning puzzles.
{: .prompt-tip }
