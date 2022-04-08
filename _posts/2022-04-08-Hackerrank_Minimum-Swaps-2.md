---
layout: post
title: "Minimum Swaps 2"
categories: programming
author:
- Nguyễn Thị Thu Hằng
---

## [Problem](https://www.hackerrank.com/challenges/minimum-swaps-2/problem?isFullScreen=true&h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays)

You are given an unordered array consisting of consecutive integers  [1, 2, 3, ..., n] without any duplicates. You are allowed to swap any two elements. Find the minimum number of swaps required to sort the array in ascending order.

#### Example
<!-- $arr = [7, 1, 3, 2, 4, 5, 6]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=arr%20%3D%20%5B7%2C%201%2C%203%2C%202%2C%204%2C%205%2C%206%5D">

Perform the following steps:
```
i   arr                         swap (indices)
0   [7, 1, 3, 2, 4, 5, 6]   swap (0,3)
1   [2, 1, 3, 7, 4, 5, 6]   swap (0,1)
2   [1, 2, 3, 7, 4, 5, 6]   swap (3,4)
3   [1, 2, 3, 4, 7, 5, 6]   swap (4,5)
4   [1, 2, 3, 4, 5, 7, 6]   swap (5,6)
5   [1, 2, 3, 4, 5, 6, 7]
```
It took 5 swaps to sort the array.

#### Function Description

Complete the function minimumSwaps in the editor below.

minimumSwaps has the following parameter(s):

int arr[n]: an unordered array of integers
#### Returns

int: the minimum number of swaps to sort the array
Input Format

The first line contains an integer n, the size of arr.
The second line contains n space-separated integers arr[i].

#### Constraints
* <!-- $1 \leq n \leq 10^5$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20n%20%5Cleq%2010%5E5">
* <!-- $1 \leq arr[i] \leq n$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20arr%5Bi%5D%20%5Cleq%20n">
#### Sample Input 0
```
4
4 3 1 2
```
#### Sample Output 0
```
3
```
#### Explanation 0
Given array <!-- $arr = [4,3,1,2]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=arr%20%3D%20%5B4%2C3%2C1%2C2%5D">

After swapping (0,2) we get <!-- $arr = [1,3,4,2]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=arr%20%3D%20%5B1%2C3%2C4%2C2%5D">

After swapping (1,2) we get <!-- $arr = [1,4,3,2]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=arr%20%3D%20%5B1%2C4%2C3%2C2%5D">

After swapping (1,3) we get <!-- $arr = [1,2,3,4]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=arr%20%3D%20%5B1%2C2%2C3%2C4%5D">

So, we need a minimum of 3 swaps to sort the array in ascending order.


#### Sample Input 1
```
5
2 3 4 1 5
```
#### Sample Output 1
```
3
```

#### Sample Input 2
```
7
1 3 5 2 4 6 7
```
#### Sample Output 2
```
3
```

## Solution
* If the position of a[i] already coincides with i+1, then ignore
* Otherwise change a[i] to the a[i]-1th position and stay in place until at position i-1 is a[i]


## Code

```c
void swap(int &a, int &b)
{
    int temp = a;
    a = b;
    b = temp;
}
// Complete the minimumSwaps function below.
int minimumSwaps(vector<int> arr) {
    int res = 0;
    for (int i=0;i<arr.size();i++)
    {
        if (arr[i]==i+1)
            continue;
        
        swap(arr[i],arr[arr[i]-1]);
        res++;
        i--;
    }
    return res;
}
```
