## Find The Longest Distance Between Each Node

```c++
#include <cstdio>
#include <vector>
#include <cstring>
#include <queue>
#include <utility>

using namespace std;
vector<pair<int,int>> a[100001];
bool check[100001];
int dist[100001];
void solution(int start) {
	
	memset(check, false, sizeof(check));
	memset(dist, 0, sizeof(dist));

	queue<int> q;
	q.push(start);
	check[start] = true;
	while (!q.empty()) {
		int node = q.front();
		q.pop();
		for (int i = 0; i < a[node].size(); i++) {
			int next = a[node][i].first;
			if (!check[next]) {
				dist[next] = dist[node] + a[node][i].second;
				q.push(next);
				check[next] = true;
			}
		}
	}
}

int main() {
	int n;

	scanf("%d", &n);

	for (int i = 0; i < n; i++) {
		int x;
		scanf("%d",&x);
		while (1) {
			int y, z;
			scanf("%d", &y);
			if (y == -1)break;
			scanf("%d", &z);
			a[x].push_back(make_pair(y, z));	
		}
	}
	solution(1);
	int start = 1;
	for (int i = 2; i <= n; i++) {
		if (dist[i] > dist[start]) {
			start = i;
		}
	}
	solution(start);
	int ans = dist[1];
	for (int i = 2; i <= n; i++) {
		if (ans < dist[i]) {
			ans = dist[i];
		}
	}
	printf("%d\n",ans);
	return 0;
}
```