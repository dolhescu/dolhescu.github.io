---
title: "POD #1 – Finding the First Occurrence of an Element in a Sorted Array"
date: 2025-09-26 10:00
categories: [Tech, Coding]
tags: [algorithm]
---

Lately, I’ve started kicking off my workday with simple coding problems—a kind of gym for the neurons. Just 10–15 minutes of focused problem-solving to wake up the brain before diving into real work. Today’s Problem of the Day (POD) is a classic one from HackerRank: finding the first occurrence of a number in a sorted array.

## Problem Statement
Given a sorted array of integers that may contain duplicates, return the index of the first occurrence of a target value or -1 if not found.

### Example
```
Input: nums = [1, 2, 3, 3, 3, 4, 5], target = 3
Output: 2
```
Explanation: The first occurrence of 3 is at index 2.

## Simple Approach: Linear Search
A straightforward solution is to iterate through the array and return the first index where the target appears:
``` csharp
public static int FindFirstOccurrenceSimple(List<int> nums, int target)
{
    for (int i = 0; i < nums.Count; i++)
    {
        if (nums[i] == target)
            return i;
    }
    return -1;
}
```

> Advantages: simple, easy to understand. Disadvantages: O(n) time complexity, which can be slow for large arrays.
{: .prompt-warning }

## Efficient Approach: Binary Search
Since the array is sorted, we can leverage binary search for an efficient O(log n) solution.

The key idea: when we find the target, we continue searching to the left to ensure we get the first occurrence.
``` csharp
public static int FindFirstOccurrence(List<int> nums, int target)
{
    int low = 0;
    int high = nums.Count - 1;
    int result = -1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (nums[mid] == target)
        {
            result = mid;      // save current index
            high = mid - 1;    // continue searching to the left
        }
        else if (nums[mid] < target)
        {
            low = mid + 1;     // search in the right half
        }
        else
        {
            high = mid - 1;    // search in the left half
        }
    }

    return result;
}
```

### How It Works
Consider the array `[1,2,3,3,3,4,5]` with `target = 3`:

1. `low=0, high=6, mid=3` → `nums[mid]=3` → save `result=3`, search left → `high=2`

2. `low=0, high=2, mid=1` → `nums[mid]=2 < target` → search right → `low=2`

3. `low=2, high=2, mid=2` → `nums[mid]=3` → save `result=2`, search left → `high=1`

4. `low > high` → stop, **first occurrence index = 2**

## Some Takeaways
- Starting the day with small problems like this is a great way to warm up your brain.
- Linear search works but is less efficient for large arrays.
- Binary search is faster (O(log n)) and, with a small adjustment, ensures the first occurrence is found even with duplicates.

> Stay tuned for monday's POD, another bite-sized brain workout to kickstart your day!.
{: .prompt-tip }
