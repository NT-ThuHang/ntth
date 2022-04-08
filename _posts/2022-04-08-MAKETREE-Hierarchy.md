---
layout: post
title: "MAKETREE - Hierarchy"
categories: programming
author:
- Nguyễn Thị Thu Hằng
---

## [Problem](https://www.spoj.com/problems/MAKETREE/)

A group of graduated students decided to establish a company; however, they don't agree on who is going to be who's boss.

Generally, one of the students will be the main boss, and each of the other students will have exactly one boss (and that boss, if he is not the main boss, will have a boss of his own too). Every boss will have a strictly greater salary than all of his subordinates - therefore, there are no cycles. Therefore, the hierarchy of the company can be represented as a rooted tree.

In order to agree on who is going to be who's boss, they've chosen K most successful students, and each of them has given a statement: I want to be the superior of him, him, and him (they could be successful or unsuccessful). And what does it mean to be a superior? It means to be the boss, or to be one of the boss' superiors (therefore, a superior of a student is not necessary his direct boss).

Help this immature company and create a hierarchy that will satisfy all of the successful students' wishes. A solution, not necessary unique, will exist in all of the test data.

Input Format
In the first line of input, read positive integers N (<!-- $N \le 100000$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=N%20%5Cle%20100000">), total number of students, and KK (<!-- $K < N$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=K%20%3C%20N">), the number of successful students. All students are numbered 1..N, while the successful ones are numbered 1..K. Then follow K lines. In <!-- $A^{th}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=A%5E%7Bth%7D">
​​  of these lines, first read an integer W (the number of wishes of the student A, <!-- $1 \le W \le 10$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=1%20%5Cle%20W%20%5Cle%2010">), and then W integers from the range [1, N] which denote students which student A wants to be superior to.

Output Format
Output N integers. The <!-- $A^{th}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=A%5E%7Bth%7D">
​​  of these integers should be 0 if student A is the main boss, and else it should represent the boss of the student A.

## Solution
Xây dựng một đồ thị có hướng không trọng số tương ứng với các nguyện vọng của K người xuất sắc nhất: có cạnh nối <!-- $u \rightarrow v$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=u%20%5Crightarrow%20v"> khi người u muốn làm cấp trên của v. Đồ thị này không có chu trình nên có thể sắp xếp Topo được. Gọi T là thứ tự Topo của đồ thị vừa xây dựng. Theo định nghĩa thì nếu có cạnh nối <!-- $u \rightarrow v$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=u%20%5Crightarrow%20v"> thì u sẽ đứng trước v trong T. Điều này có nghĩa là với mỗi người u, tất cả những người cấp dưới mà u muốn đều nằm sau u trong T.

Cách xây dựng cây phân cấp đơn giản nhất là xây dựng theo thứ tự T:

* <!-- $T_1$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_1"> làm sếp tổng <!-- $\leftrightarrow boss(T_1) = -1$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cleftrightarrow%20boss(T_1)%20%3D%20-1">
* Sếp của <!-- $T_2$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_2"> là <!-- $T_1$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_1">
​<!-- $\leftrightarrow boss(T_2) = T_1$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cleftrightarrow%20boss(T_2)%20%3D%20T_1">
* Sếp của <!-- $T_3$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_3"> là <!-- $T_2 \leftrightarrow boss(T_3) = T_2$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_2%20%5Cleftrightarrow%20boss(T_3)%20%3D%20T_2">
* ...
* Sếp của <!-- $T_N$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_N"> là <!-- $T_{N-1} \leftrightarrow boss(T_N) = T_{N-1}$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=T_%7BN-1%7D%20%5Cleftrightarrow%20boss(T_N)%20%3D%20T_%7BN-1%7D">

Cuối cùng mảng boss chính là kết quả cần xuất ra màn hình.

Độ phức tạp: <!-- $\mathcal{O} \left( N + sum({W_i}) \right)$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=%5Cmathcal%7BO%7D%20%5Cleft(%20N%20%2B%20sum(%7BW_i%7D)%20%5Cright)">. với <!-- $N$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=N"> là số người trong công ty và <!-- $W_i$ --> <img style="transform: translateY(0.1em); background: white;" src="https://render.githubusercontent.com/render/math?math=W_i"> là số người cấp dưới mà người i chọn.

## [Code](https://github.com/NT-ThuHang/Practice-Coding-Skill/blob/main/BigO_Orange06/Topic%2001:%20Topological%20Sort/Hierarchy/Hierarchy.cpp)
```c
#include <bits/stdc++.h>
using namespace std;

void dfs(int u, const vector<vector<int>> &graph, vector<bool> &visited, vector<int> &result) {
    visited[u] = true;
    for (int i = 0; i < graph[u].size(); i++) {
        int v = graph[u][i];
        if (!visited[v]) {
            dfs(v, graph, visited, result);
        }
    }
    result.push_back(u);
}

vector<int> topologicalSort(const vector<vector<int>> &graph) {
    int V = graph.size();
    vector<int> result;
    result.reserve(V);
    vector<bool> visited(V, false);

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            dfs(i, graph, visited, result);
        }
    }
    std::reverse(result.begin(), result.end());
    return result;
}

int main() {
    int n, k;
    scanf("%d%d", &n, &k);
    vector<vector<int>> graph(n);
    for (int u = 0; u < k; ++u) {
        int w, v;
        scanf("%d", &w);
        while (w--) {
            scanf("%d", &v);
            graph[u].push_back(v - 1);
        }
    }

    auto topo_order = topologicalSort(graph);
    vector<int> boss(n);
    boss[topo_order[0]] = -1;
    for (int i = 1; i < n; ++i) {
        boss[topo_order[i]] = topo_order[i - 1];
    }
    
    for (int i = 0; i < n; ++i) {
        printf("%d\n", boss[i] + 1);
    }
}
```