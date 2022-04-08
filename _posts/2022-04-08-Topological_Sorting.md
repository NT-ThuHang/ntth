---
layout: post
title: "TOPOSORT - Topological Sorting"
categories: programming
author:
- Nguyễn Thị Thu Hằng
---

## [Problem](https://www.hackerrank.com/challenges/crush/problem?isFullScreen=true&h_l=interview&playlist_slugs%5B%5D=interview-prepa)

Sandro is a well organised person. Every day he makes a list of things which need to be done and enumerates them from 1 to n. However, some things need to be done before others. In this task you have to find out whether Sandro can solve all his duties and if so, print the correct order.

#### Input

In the first line you are given an integer n and m (1<=n<=10000, 1<=m<=1000000). On the next m lines there are two distinct integers x and y, (1<=x,y<=10000) describing that job x needs to be done before job y.

#### Output

Print "Sandro fails." if Sandro cannot complete all his duties on the list. If there is a solution print the correct ordering, the jobs to be done separated by a whitespace. If there are multiple solutions print the one, whose first number is smallest, if there are still multiple solutions, print the one whose second number is smallest, and so on.

#### Example 1
```
Input:
8 9
1 4
1 2
4 2
4 3
3 2
5 2
3 5
8 2
8 6
Output:
1 4 3 5 7 8 2 6 
```

## Solution

Ta xem N công việc là N đỉnh của đồ thị, còn M cặp công việc là M cạnh của đồ thị có hướng. Vì một số công việc sẽ thực hiện trước một vài công việc khác nên ta sẽ dùng Topological Sort để giải quyết bài toán này. Nhận xét :

Sandro sẽ không thực hiện được tất cả công việc nếu xuất hiện chu trình trong đồ thị.
Do yêu cầu đặc biệt nếu có nhiều công việc có cùng thứ tự thực hiện thì ta chọn công việc có số nhỏ nhất. Vậy để luôn chọn được công việc có số thứ tự nhỏ nhất thực hiện lúc đó ta cần cấu trúc dữ liệu thích hợp, ở đây ta chọn thuật toán Kahn và min heap để lưu các đỉnh có thể được chọn tiếp.
Vậy với thuật toán Kahn, ta cần danh sách đỉnh kề, mảng đếm số bậc vào còn lại của mỗi đỉnh và min heap các đỉnh có bậc vào hiện tại bằng 0.

Ta bắt đầu với việc xác định các đỉnh có số bậc vào bằng 0 và cho vào heap.
Khi mà heap vẫn còn các đỉnh chưa được xét, ta chọn đỉnh đầu tiên trong heap sẽ là đỉnh tiếp theo được in ra.
Đồng thời, khi đỉnh này được chọn ta giảm đi số bậc vào của các đỉnh kề từ đỉnh này. Nếu có bất kì đỉnh kề nào có bậc vào bằng 00 thì ta cho đỉnh này vào heap.
Kết quả cuối cùng sau khi kết thúc thuật Kahn sẽ là danh sách các công việc cần thực hiện theo thứ tự thỏa mãn.
Độ phức tạp: <!-- $\mathcal{O} \left( N \cdot \log(N) + M \right)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cmathcal%7BO%7D%20%5Cleft(%20N%20%5Ccdot%20%5Clog(N)%20%2B%20M%20%5Cright)"> với N là số công việc cần thực hiện, M là số cặp công việc phải thực hiện theo đúng thứ tự.

## [Code](https://github.com/NT-ThuHang/Practice-Coding-Skill/blob/main/BigO_Orange06/Topic%2001:%20Topological%20Sort/Topological%20Sorting/Topo_Sort.cpp) 

```c

#include <iostream>
#include <vector>
#include <queue>
#include <set>

using namespace std;

vector<int> topoSort(vector< vector<int> > &adj, vector<int> &indegree){
    int n = indegree.size();
    priority_queue<int, vector<int>, greater<int> > zero_indegree;
    vector<int> topoSorted;
    // vector<bool> avail(n, true);

    for (int i = 0; i < indegree.size(); i++)
        if (indegree[i] == 0){
            zero_indegree.push(i);
            // avail[i] = false;
        }


    while (!zero_indegree.empty()){
        int u = zero_indegree.top();
        zero_indegree.pop();

        topoSorted.push_back(u);

        for (int i = 0;i < adj[u].size(); i++){
            int v = adj[u][i];
            indegree[v] --;
            if (indegree[v] == 0){
                zero_indegree.push(v);
            }
        }
    }

    
    return topoSorted;
}

int main(){
    // n: number of vertices
    // m: number of edges
    int n, m, u, v;
    vector< vector<int> > adj;
    vector<int> indegree;
    scanf("%d %d", &n, &m);
    adj.resize(n);
    indegree.assign(n, 0);
    for (int i = 0; i < m; i++){
        scanf("%d %d", &u, &v);
        adj[u - 1].push_back(v - 1);
        indegree[v - 1] ++;
    }
    
    vector<int> res = topoSort(adj, indegree);
    if (res.size() < n){
        printf("Sandro fails.\n");
        return 0;
    }

    for (int i = 0; i < res.size(); i++)
        printf("%d ", res[i] + 1);
    printf("\n");

    return 0;
}
```
