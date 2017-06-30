# **Dynamic Programing**



<u>인접한 집을 동일한 색으로 색칠하지 않고 최소 Cost 구하기.</u>

```c
#include <stdio.h>
int min(int a, int b);
int main() {

	int arr[3];
	int cost[1000][3] = { 0, };
	int N;

	scanf("%d", &N);
	scanf("%d %d %d", &cost[0][0], &cost[0][1], &cost[0][2]);

	for (int i = 1; i < N; i++) {
		scanf("%d %d %d", &arr[0], &arr[1], &arr[2]);
		cost[i][0] = min(cost[i - 1][1], cost[i - 1][2]) + arr[0];
		cost[i][1] = min(cost[i - 1][0], cost[i - 1][2]) + arr[1];
		cost[i][2] = min(cost[i - 1][0], cost[i - 1][1]) + arr[2];
	}
	printf("%d\n", min(min(cost[N - 1][0], cost[N - 1][1]), cost[N - 1][2]));

	return 0;
}
int min(int a, int b) {
	if (a > b)
		return b;
	else
		return a;
}
```



