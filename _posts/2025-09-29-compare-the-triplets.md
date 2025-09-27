---
title: "POD #2 – Compare the Triplets"
date: 2025-09-29 08:00
categories: [Tech, Coding]
tags: [algorithm]
---

It’s Monday again, which means it’s time for a new Problem of the Day. Today we’ll solve a well-known exercise called Compare the Triplets.

## Problem Statement
Alice and Bob each created one problem for HackerRank. A reviewer rates the two challenges, awarding points on a scale from **1 to 100** for three categories:
- Problem clarity
- Originality
- Difficulty

The rating for Alice’s challenge is the triplet `a = (a[0], a[1], a[2])`, and the rating for Bob’s challenge is `b = (b[0], b[1], b[2])`.
The task is to calculate their comparison points:
- If `a[i] > b[i]`, then Alice is awarded 1 point.
- If `a[i] < b[i]`, then Bob is awarded 1 point.
- If `a[i] == b[i]`, then no points are awarded.

At the end, we return an array `[alicePoints, bobPoints]`.

### Example
```
a = [1, 2, 3]
b = [3, 2, 1]
```
- At index 0: `a[0] < b[0]` → Bob earns 1 point
- At index 1: `a[1] == b[1]` → no points
- At index 2: `a[2] > b[2]` → Alice earns 1 point

Result: `[1, 1]`

## Try It Yourself
Before reading further, I strongly encourage you to try solving the exercise directly on [HackerRank](https://www.hackerrank.com/challenges/compare-the-triplets/problem).
Give it a shot, then come back here to compare your solution with mine. This practice of attempting first and reviewing later will sharpen your problem-solving skills much faster.

## My Approach
The problem is straightforward: we just need to loop through the three elements, compare each value, and update the scores.

Since the input size is fixed (exactly 3 comparisons), both time and space complexity are constant:
- Time complexity: `O(1)`
- Space complexity: `O(1)`

## Solution in C#
Here’s my implementation in C#:
``` csharp
public static List<int> CompareTriplets(List<int> a, List<int> b)
{
    int alicePoints = 0;
    int bobPoints = 0;

    for (int i = 0; i < 3; i++)
    {
        if (a[i] > b[i])
        {
            alicePoints++;
        }
        if (a[i] < b[i])
        {
            bobPoints++;
        }
    }

    return new List<int> { alicePoints, bobPoints };
}

```
## Some Takeaways
- A clean solution doesn’t always mean a complex algorithm. Sometimes the simplest problems remind us to focus on clarity and correctness.
- Using two independent if statements keeps the logic straightforward and readable.
- It’s always good practice to test edge cases.

> This post is part of my Problem of the Day series, where I solve one coding challenge each weekday and share my approach, solutions, and takeaways. See you in the next Problem of the Day!
{: .prompt-tip }
