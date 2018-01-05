```c++
//완전탐색 dfs
#include <cstdio>
#include <algorithm>
#include <utility>
#include <vector>
using namespace std;
int n;
int answer;
pair<int, int> company,home;
bool chk[11];

int distance(pair<int, int> p1, pair<int, int> p2) {
	return abs(p1.first - p2.first) + abs(p1.second - p2.second);
}
void solution(vector<pair<int,int>> p, int depth, int dist, int idx) {

	if (depth == n - 1) {
		dist += distance(p[idx], home);
		answer = min(dist, answer);
		return;
	}

	if (answer < dist)return;

	for (int i = 0; i < n; i++) {
		if (chk[i]) continue;

		chk[i] = true;
		solution(p, depth + 1, dist + distance(p[idx],p[i]), i);
		chk[i] = false;
		
	}
	return;
}
int main() {
	int T;
	scanf("%d",&T);
	for (int test_case = 0; test_case < T; test_case++) {
		answer = 9999999;
		scanf("%d", &n);
		vector<pair<int, int>> point;
		scanf("%d %d", &company.first, &company.second);
		scanf("%d %d", &home.first, &home.second);
		for (int i = 0; i < n; i++) {
			pair<int, int> tmp;
			scanf("%d %d", &tmp.first, &tmp.second);
			point.push_back(tmp);			
		}
		for (int i = 0; i < n; i++) {
			int dist = distance(company, point[i]);
			chk[i] = true;
			solution(point, 0, dist, i);
			chk[i] = false;
		}
		printf("#%d %d\n", test_case + 1, answer);
	}
	return 0;
}


```

