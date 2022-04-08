---
layout: post
title: "[HackerRank] New Year Chaos"
categories: programming
author:
- Nguyễn Thị Thu Hằng
---

## [Problem](https://www.hackerrank.com/challenges/new-year-chaos/problem?isFullScreen=true&h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays)

It is New Year's Day and people are in line for the Wonderland rollercoaster ride. Each person wears a sticker indicating their initial position in the queue from 1 to n . Any person can bribe the person directly in front of them to swap positions, but they still wear their original sticker. One person can bribe at most two others.

Determine the minimum number of bribes that took place to get to a given queue order. Print the number of bribes, or, if anyone has bribed more than two people, print Too chaotic.

#### Example
<!-- $q = [1,2,3,5,4,6,7,8]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=q%20%3D%20%5B1%2C2%2C3%2C5%2C4%2C6%2C7%2C8%5D">

If person 5 bribes person 4, the queue will look like this: 1,,2,3,5,4,6,7,8 . Only 1 bribe is required. Print 1.

<!-- $q = [4,1,2,3]$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=q%20%3D%20%5B4%2C1%2C2%2C3%5D">
Person 4 had to bribe 3 people to get to the current position. Print Too chaotic.

#### Function Description

Complete the function minimumBribes in the editor below.

minimumBribes has the following parameter(s):

int q[n]: the positions of the people after all bribes
#### Returns

No value is returned. Print the minimum number of bribes necessary or Too chaotic if someone has bribed more than 2 people.
#### Input Format

The first line contains an integer t, the number of test cases.

Each of the next t pairs of lines are as follows:
- The first line contains an integer t, the number of people in the queue
- The second line has n space-separated integers describing the final state of the queue.

#### Constraints
* <!-- $1 \leq t \leq 10$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20t%20%5Cleq%2010">
* <!-- $1 \leq n \leq 10^5$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20n%20%5Cleq%2010%5E5">
#### Subtasks

For <!-- $60\%$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=60%5C%25"> score <!-- $1 \leq n \leq 10^3$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20n%20%5Cleq%2010%5E3"> 

For <!-- $100\%$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=100%5C%25"> score <!-- $1 \leq n \leq 10^5$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cleq%20n%20%5Cleq%2010%5E5">

Sample Input
```
STDIN       Function
-----       --------
2           t = 2
5           n = 5
2 1 5 3 4   q = [2, 1, 5, 3, 4]
5           n = 5
2 5 1 3 4   q = [2, 5, 1, 3, 4]
```
Sample Output
```
3
Too chaotic
```

## Solution
* For each element to the number of elements greater than it is in front of it, this is simply understood that the person in the back wants to move forward.

* If the position after shifting forward 3 units, the printout is too chaotic.
## Code

```c
void minimumBribes(vector<int> q) 
{
    int total=0;
    for (int i = q.size()-1;i>=0;i--)
    {
        if (q[i]-i-1 > 2)
        {
            cout << "Too chaotic \n";
            return;
        }
        for (int j = max(0,q[i]-2);j<i;j++)
        {
            if (q[j]>q[i])
                total++;
        }
    }
    cout << total << "\n";
}
```