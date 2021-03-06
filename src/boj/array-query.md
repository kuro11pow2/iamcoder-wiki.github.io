# BOJ/수열과 쿼리
## 수열과 쿼리 0
[문제](https://www.acmicpc.net/problem/13545)

\\(S_i = A_1 + A_2 + ... + A_i\\)로 정의하면 쿼리 \\(i j\\)가 주어지면 \\(S_x = S_y\\)이고 \\(i-1 \leq x < y \leq j\\)인 \\(x, y\\)에 대해 \\(y-x\\)의 최댓값을 구하면 된다. 이는 [[ Mo's Algorithm ]]을 사용하여 각 \\(k\\)에 대해 \\(S_i = k\\)인 \\(i\\)들을 [[ Deque ]]로 저장하고 그 [[ Deque ]]들에서 가장 첫 원소와 가장 마지막 원소의 차들를 [[ Priority Queue ]]로 관리하여 답을 구할 때마다 [[ Priority Queue ]]에 존재하는 값들 중 최댓값을 선택하면 된다.

## 수열과 쿼리 1
[문제](https://www.acmicpc.net/problem/13537)

같은 문제를 온라인으로 처리하는 문제가 수열과 쿼리 3번 문제이므로 수열과 쿼리 1은 오프라인 쿼리를 처리하는 풀이로 설명한다.

\\((i, j, k)\\) 쿼리들을 \\(k\\)가 큰 순으로 내림차순 정렬한 것을 순서대로 \\((i_1, j_1, k_1), ..., (i_M, j_M, k_M)\\)라 하고 입력에 주어진 수열로 `pair<int, int>` \\((i, A_i)\\)를 만들어 \\(A_i\\)가 큰 순으로 내림차순 정렬한 것을 \\((x_1, y_1), ..., (x_N, y_N)\\)으로 표현하자. \\(n\\)번째 쿼리 \\((i_n, j_n, k_n)\\)을 처리하기 위해서 *아직 업데이트하지 않은 가장 앞 \\((x_m, y_m)\\)를 잡아 만약 \\(y_m>k_n\\)일 경우 [[ Segment Tree ]] \\(x_m\\)번째 자리에 1을 더하는 업데이트를 하는 과정*을 반복해주자. 이후 쿼리의 답은 [[ Segment Tree ]]에서 \\(i_n\\)과 \\(j_n\\) 사이 구간 합을 구하면 쉽게 구할 수 있다.


## 수열과 쿼리 1.5
[문제](https://www.acmicpc.net/problem/17410)

수열과 쿼리 1에 \\(A_i\\)를 \\(v\\)로 바꾸는 쿼리가 추가된 문제다. 

[[ Sqrt Decomposition ]]을 사용하면 풀 수 있다. 원소를 \\(\sqrt{N}\\)개씩 묶어서 정렬된 상태로 갖고 있으면 각 쿼리를 다음과 같이 처리할 수 있다.

1. **Update** : 원소의 값을 바꾸고, 바꾼 원소가 포함된 묶음의 정렬된 상태에서 \\(O(\sqrt{N})\\)에 기존 원소를 삭제하고 새로운 원소를 추가하는 연산을 해줄 수 있다.
2. **Calc** :  묶음 단위로 구간에 포함되어 있는 경우, 해당 묶음에서 \\(k\\)보다 큰 원소의 개수를 [[ Binary Search ]]로 쉽게 구할 수 있으며, 묶음 단위로 포함되진 않지만 구간에 포함되는 최대 \\(2\sqrt{N}\\)개의 원소는 일일이 순회하면서 \\(k\\)보다 큰 원소의 개수를 구해주면 된다.

이 경우 문제를 \\(O(N\sqrt{N})\\)이라는 시간복잡도로 풀 수 있다.

## 수열과 쿼리 2
[문제](https://www.acmicpc.net/problem/13543)


## 수열과 쿼리 3
[문제](https://www.acmicpc.net/problem/13544)

수열과 쿼리 1과 같은 문제를 온라인 쿼리로 처리하는 문제다.

[[ Merge Sort Tree ]]를 사용하면 [[ Segment Tree ]]와 비슷한 구조에서 특정 구간에 포함된 원소들을 정렬된 상태로 저장할 수 있다. 이를 이용하면 \\(i, j, k\\) 쿼리가 들어오면 \\((i, j)\\)를 포함하는 [[ Merge Sort Tree ]]의 구간 \\(\log N\\)개에서 [[ Binary Search ]]를 해서 \\(k\\)보다 큰 원소의 개수를 구할 수 있다.

[[ Persistent Segment Tree ]]를 사용해서도 풀 수 있다. \\(i\\)번째 [[ Persistent Segment Tree ]]에서 \\(j\\)번째 위치에 \\(A_1\\)부터 \\(A_i\\) 중 값이 \\(j\\)인 수[^1]들의 개수를 저장하는 구간 합 [[ Persistent Segment Tree ]]를 만들면 \\(i, j, k\\)를 처리할 때 \\(j\\)번째 [[ Persistent Segment Tree ]]에서 \\(k\\)보다 큰 수의 개수에서 \\(i-1\\)번째 [[ Persistent Segment Tree ]]에서 \\(k\\)보다 큰 수의 개수를 빼주면 답을 구할 수 있다.

## 수열과 쿼리 4
[문제](https://www.acmicpc.net/problem/13546)

수열과 쿼리 0과 동일한 방법으로 풀 수 있다.

## 수열과 쿼리 5
[문제](https://www.acmicpc.net/problem/13547)

[[ Mo's Algorithm ]]을 기본적으로 사용해야 하며, 구간 이동 과정에서 각 \\(k\\)에 대해 구간 내 존재하면서 원소 값이 \\(k\\)인 원소 개수를 관리하면 있으면 현재 구간에 존재하는 서로 다른 수의 개수를 저장하고 있을 수 있다.

## 수열과 쿼리 6
[문제](https://www.acmicpc.net/problem/13548)

[[ Mo's Algorithm ]]을 사용해서 각 \\(k\\)에 대해 구간 내 존재하는 값이 \\(k\\)인 원소 개수를 관리하면 [[ Priority Queue ]]를 통해 구간에서 가장 많이 등장하는 수가 몇번 등장하는지 구할 수 있다.

## 수열과 쿼리 7
[문제](https://www.acmicpc.net/problem/13550)

수열과 쿼리 1.5과 동일한 방법으로 풀 수 있는데, \\(S_i\\)를 \\(A_1 + A_2 + ... + A_i\\)를 \\(K\\)로 나눈 나머지로 정의하면 된다.

## 수열과 쿼리 8
[문제](https://www.acmicpc.net/problem/13553)

\\(i\\)번째 위치에 원소의 값이 \\(i\\)인 원소 개수를 저장하는 구간 합 [[ Segment Tree ]]를 이용하여 [[ Mo's Algorithm ]]를 사용하여 현재 관리하는 구간에 원소 \\(A_i\\)가 추가될 때마다 절댓값 차이가 \\(K\\) 이하인 구간 \\([A_i-K, A_i+K]\\)의 원소 개수를 [[ Segment Tree ]]에서 구하여 답안에 더해주는 과정을 한 다음,  추가되는 원소에 대해서 [[ Segment Tree ]]에 업데이트를 해주는 과정을 반복하면 된다.

## 수열과 쿼리 9
[문제](https://www.acmicpc.net/problem/13554)

[[ Mo's Algorithm ]]을 사용하여 어떤 쿼리 \\(i, j, k\\)을 처리할 때 \\\(n\\)번째 위치에 \(A_i, A_i+1, ..., A_j\\) 중 \\(n\\)의 개수를 저장하는 구간 합 [[ Segment Tree ]]와, 마찬가지로 \\(B_i, B_i+1, ..., B_j\\) 중 \\(n\\)의 개수를 저장하는 구간 합 [[ Segment Tree ]]를 \\(O(N\sqrt{N}\log N)\\) 시간복잡도로 관리할 수 있다. 이후 \\(i, j, k\\)를 처리하는 방법은 \\(A_p \times B_q \leq k\\)이면 \\(A_p \leq \sqrt{k}\\) 또는 \\(B_q \leq \sqrt{k}\\)라는 사실을 이용하여 \\(\sqrt{k}\\)만큼 반복하면서 \\(A_p, B_q\\) 중 작은 값을 고정시켰을 때 큰 값이 될 수 있는 수들의 개수를 계산해주면서 쿼리마다 \\(O(\sqrt{k}\log N)\\) 시간복잡도로 구하면 된다. [^2]

## 수열과 쿼리 10
[문제](https://www.acmicpc.net/problem/13557)

\\(S_i = A_1 + A_2 + ... + A_i\\)라 하면 쿼리 \\(x1, y1, x2, y2\\)는 \\(x1-1 \leq s \leq y1-1, x2 \leq e \leq y2, s < e\\)인 \\(s, e\\)에 대해 \\(S_e-S_s\\)의 최댓값을 출력하면 된다. \\([x1-1, y1-1]\\) 구간과 \\([x2, y2]\\) 구간이 겹치지 않으면 구간 최댓값과 최솟값을 저장하는 [[ Segment Tree ]]로 쉽게 구할 수 있다.

 \\([x1-1, y1-1]\\) 구간과 \\([x2, y2]\\) 구간이 \\([x2, y1-1]\\)에서 겹치면 시작점과 끝점의 구간이 겹치지 않는 두 상태 (\\(s \in [x1-1, x2-1], e\in [x2, y2]\\) , \\(s \in [x1-1, y1-1], e\in [y1, x2]\\))에서 위와 같이 구한 다음 시작점과 끝점 모두 \\([x2, y1-1]\\) 안에 속하는 경우를 추가적으로 고려해주면 된다. 이는 구간 최댓값과 최솟값을 저장한 [[ Segment Tree ]]에 현재 구간 내부에 시작점과 끝점 모두 존재할 경우 \\(S_e - S_s\\)의 최댓값을 추가적으로 저장하면 처리할 수 있다.



----

[^1]: [[ Grid Compression ]]을 해야된다

[^2]: [[ Segment Tree ]]를 쓰면 시간 초과가 날 수 있기 때문에 [[ Fenwick Tree ]]를 써야 할 수도 있다.
