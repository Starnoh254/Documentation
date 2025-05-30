---
title: Look How Far I've Come Journal
date: 2025-05-23
description: Personal journal entry reflecting on solving the "Max Area of Island" problem, including solution breakdown, insights, and growth in DSA.
tags: [Journal, DSA, Growth, Problem Solving, Max Area of Island, DFS, Coding]
---

# Look How Far I've Come Journal 🚀
**Date:** 2025-05-23 14:44:11


## 🎉 Milestone: Solved "Max Area of Island" on First Try!

Brooo 🔥🔥🔥 congrats!! Solving **"Max Area of Island"** on your **first try** is no joke — that’s actual growth right there.

---

### 🚀 Problem Recap
You're given a grid where:
- `1` represents **land**
- `0` represents **water**

Your job is to find the **largest island** (group of connected 1s — horizontally or vertically).

---

### 🔍 High-Level Idea
Loop through the grid. When a `1` is found:
- Trigger a **DFS** to explore the island and count the area
- Update `maxArea` if this one is the biggest so far

---

### 🧠 Solution Breakdown

```cpp
int maxArea = 0;
```

- Initialize largest area as 0.

```cpp
for(int i = 0 ; i < grid.size() ; i ++){
    for(int j = 0 ; j < grid[0].size(); j++){
        if(grid[i][j] == 1){
            int area = dfs(grid , i , j);
            if(area > maxArea){
                maxArea = area;
            }
        }
    }
}
```

- Scan every cell
- On finding a `1`, use DFS to get island area
- Update `maxArea` accordingly

```cpp
int dfs(vector<vector<int>>& grid , int i , int j){
    int w = grid.size();
    int h = grid[0].size();
    int area = 0;

    if(i < 0 || i >= w || j < 0 || j >= h || grid[i][j] == 0){
        return 0;
    }

    area += 1;
    grid[i][j] = 0;

    int totalArea = 
    dfs(grid , i + 1 , j) + 
    dfs(grid , i - 1 , j) + 
    dfs(grid , i  , j + 1) + 
    dfs(grid , i , j - 1);

    area += totalArea;

    return area;
}
```

- Base case: return if out of bounds or water
- Visit the cell, mark it `0` (visited), count it
- Recurse in all 4 directions
- Sum up area

---

### ✅ Why this works

This is a **flood-fill** algorithm (like the paint bucket tool). DFS explores deeply and counts each land cell exactly once.

---

### 🔥 What Went Right
- Clear base case
- Correct in-bounds checking
- Clean DFS logic
- Avoided extra space
- Smart area tracking

---

### 🧙‍♂️ Becoming a Wizard
Doing DSA daily rewires your brain to see patterns. You’re not just solving problems — you’re learning to think deeply and write clean code like a boss.

Keep going bro 💪 this is just the beginning.
