---
title: "POD #3 – Grading Students"
date: 2025-09-29 10:00
categories: [Tech, Coding]
tags: [algorithm]
---

It’s Tuesday, the second day of the week, but we are already at Problem #3. That’s because I started this series last Friday, following a simple principle of motivation and discipline: *start today, not tomorrow*. Don’t wait for Monday to begin.  

These small “imperfections”, breaking away from routines and patterns, are exactly what I enjoy. They remind me that we are all human.  

> And here’s a small confession: there may be days when I won’t publish a *Problem of the Day*. Some days will simply be too packed with production work. But that doesn’t mean I can’t return the next day with the same energy and consistency. With that disclaimer out of the way, let’s get to today’s challenge.
> {: .prompt-warning }


## Problem Statement

**HackerLand University** has the following grading policy:

- Any grade less than 40 is a failing grade.  
- If the difference between a grade and the next multiple of 5 is less than 3, round the grade up to that multiple.  
- Otherwise, leave the grade unchanged.  

**Examples**:
- 84 → 85  
- 29 → 29  
- 57 → 57  

**Task**: Implement a function that applies this rounding policy to a list of student grades.


## Try It Yourself
If you want to solve this challenge yourself, try it here first: [HackerRank – Grading Students](https://www.hackerrank.com/challenges/grading/problem)


## My Solution (C#)

```csharp
public static List<int> gradingStudents(List<int> grades)
{
    List<int> gradesAfterRounding = new List<int>();
    
    foreach (var grade in grades)
    {
        if (grade < 38)
        {
            gradesAfterRounding.Add(grade);
        }
        else
        {
            int nextMultiple = grade + (5 - grade % 5);
            if (nextMultiple - grade < 3)
                gradesAfterRounding.Add(nextMultiple);
            else
                gradesAfterRounding.Add(grade);    
        }
    }
    return gradesAfterRounding;
}
```
### Example Walkthrough

Let’s test the function with a few sample grades:

- `73 → 75` The next multiple of `5 is 75`. `Difference = 2`, so the grade is rounded up.
- `67 → 67` The next multiple of `5 is 70`. `Difference = 3`, so the grade stays the same.
- `38 → 40` The next multiple of `5 is 40`. `Difference = 2`, so the grade is rounded up.
- `33 → 33` Below 38, so no rounding occurs.

### Complexity Analysis
- Time Complexity: O(n), where n is the number of students, since we process each grade once
- Space Complexity: O(n), for storing the final list of rounded grades.

> In today’s AI era, where many juniors rely on generated code without fully understanding how it works, I believe it’s more important than ever to return to the fundamentals and keep our minds sharp. Stay tuned for the next Problem of the Day!
{: .prompt-tip }
