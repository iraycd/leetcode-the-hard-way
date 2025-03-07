---
description: 'Author: @wingkwong | https://leetcode.com/problems/rotate-image/'
tags: [Array, Math, Matrix]
---

# 0048 - Rotate Image (Medium) 

## Problem Statement

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```

**Example 2:**

```
Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

## Approach 1: Rotate 4 Cells in a Round

<SolutionAuthor name="@wingkwong"/>

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        // round 1: 
        // -------------------
        // tmp <- 1
        // top left cell matrix[i][j] (1) <- bottom left 7 cell (matrix[n - j - 1][i])
        // bottom left 7 cell (matrix[n - j - 1][i]) <- bottom right cell 9 (matrix[n - i - 1][n - j - 1])
        // bottom right cell 9 (matrix[n - i - 1][n - j - 1]) <- top right cell 3 (matrix[j][n - i - 1])
        // top right cell 3 (matrix[j][n - i - 1]) <- 1 (tmp)

        // 1 2 3    7 2 1
        // 4 5 6 => 4 5 6
        // 7 8 9    9 8 7

        // // round 2:
        // -------------------
        // tmp <- 2
        // 2 (matrix[i][j]) <- 4 (matrix[n - j - 1][i])
        // 4 (matrix[n - j - 1][i]) <- 8 (matrix[n - i - 1][n - j - 1])
        // 8 (matrix[n - i - 1][n - j - 1]) <- 6 (matrix[j][n - i - 1])
        // 6 (matrix[j][n - i - 1]) <- 2 (tmp)

        // 1 2 3    7 2 1    7 4 1
        // 4 5 6 => 4 5 6 => 8 5 2
        // 7 8 9    9 8 7    9 6 3
        int n = matrix.size(), tmp;
		for(int i = 0; i < n / 2; i++) {
            for(int j = i; j < n - i - 1; j++) {
				tmp = matrix[i][j];
				matrix[i][j] = matrix[n - j - 1][i];
				matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1];
				matrix[n - i - 1][n - j - 1] = matrix[j][n - i - 1];
				matrix[j][n - i - 1] = tmp;
			}
        }
			
    }
};

```