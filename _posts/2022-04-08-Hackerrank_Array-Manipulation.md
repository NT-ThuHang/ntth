---
layout: post
title: "Array Manipulation"
categories: programming
author:
- Nguyễn Thị Thu Hằng
---

## [Problem](https://www.hackerrank.com/challenges/crush/problem?isFullScreen=true&h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays)
Starting with a 1-indexed array of zeros and a list of operations, for each operation add a value to each the array element between two given indices, inclusive. Once all operations have been performed, return the maximum value in the array.

#### Example

Queries are interpreted as follows:

    a b k
    1 5 3
    4 8 7
    6 9 1
Add the values of  between the indices  and  inclusive:
```
index->	 1 2 3  4  5 6 7 8 9 10
	[0,0,0, 0, 0,0,0,0,0, 0]
	[3,3,3, 3, 3,0,0,0,0, 0]
	[3,3,3,10,10,7,7,7,0, 0]
	[3,3,3,10,10,8,8,8,1, 0]
```

The largest value is  after all operations are performed.

#### Function Description

Complete the function arrayManipulation in the editor below.

arrayManipulation has the following parameters:

int n - the number of elements in the array
int queries[q][3] - a two dimensional array of queries where each queries[i] contains three integers, a, b, and k.
#### Returns

int - the maximum value in the resultant array
#### Input Format

The first line contains two space-separated integers  and , the size of the array and the number of operations.
Each of the next  lines contains three space-separated integers ,  and , the left index, right index and summand.

#### Constraints
* <!-- $3 \leq n \leq 10^7$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=3%20%5Cleq%20n%20%5Cleq%2010%5E7">

* <!-- $1 \leq m \leq 2*10^5$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20m%20%5Cleq%202*10%5E5">

* <!-- $1 \leq a \leq b \leq n$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20a%20%5Cleq%20b%20%5Cleq%20n">

* <!-- $0 \leq k \leq 10^9$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=0%20%5Cleq%20k%20%5Cleq%2010%5E9">

#### Sample Input
```
5 3
1 2 100
2 5 100
3 4 100
```
#### Sample Output
```
200
```
#### Explanation

After the first update the list is 100 100 0 0 0.

After the second update list is 100 200 100 100 100.

After the third update list is 100 200 200 200 100.

The maximum value is **200**.

## Solution
* Assign the array value at position a is k and position b+1 is -k, this we can simply understand that when we go on the segment [a,b] the value will be k and if we get out of it will subtract k.

* After that, we only need to find the segment with the largest sum in the sequence with n elements.

#### Example:
##### Input:
```
10 3
1 5 3
4 8 7
6 9 1
```
##### Output:
```
10
```
##### Solve:
* Begin:
```
arr[10] = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
* With query 0: the segment [a,b] is [1,5] and k is 3
```
arr[10] = [3, 0, 0, 0, 0, -3, 0, 0, 0, 0]
```
* With query 0: the segment [a,b] is [4,8] and k is 7
```
arr[10] = [3, 0, 0, 7, 0, -3, 0, 0, -7, 0]
```
* With query 0: the segment [a,b] is [6,9] and k is 1
```
arr[10] = [3, 0, 0, 7, 0, -2, 0, 0, 0, -1]
```
* End: the result is the largest sum of array.

## Code

```c
int main()
{
    long n,m;
    cin >> n >> m;
    vector < vector<long> > queries;
    vector <long> arr (n+1, 0);
    long a, b, k,res = 0;
    for (long i=0; i<m; i++)
    {
        cin >> a >> b >> k;
        arr[a-1] += k;
        arr[b] += -k;
    }
    long tmp = 0;
    for (int i=0; i<n; i++)
    {
        //cout << arr[i] << " ";
        tmp += arr[i];
        res = max(res, tmp);
    }
    cout << res;
    return 0;
}
```
