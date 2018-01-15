```c++
/*
DFS 완탐, O(4^n), 
코어가 가장자리 있을 경우 연산 단축 가능.
조건 실수하지 말기.
*/
#include <cstdio>
#include <vector>
#include <utility>
#include <algorithm>

using namespace std;
int a[12][12];
int n;
int dx[] = { 1, 0, -1, 0 };
int dy[] = { 0, 1, 0, -1 };
int maxCnt = 0;
int minLen = 9999999;
vector<pair<int,int>> core;
int length;
void solution(int map[12][12], int coreIdx, int coreCnt, int lineLen) {
	//모든 코어를 다 봤을 때,
	if (coreIdx == n) {
		if (maxCnt < coreCnt) { //코어수가 많으면 갱신
			maxCnt = coreCnt;
			minLen = lineLen;
		}
		if ((maxCnt <= coreCnt && lineLen < minLen)) //코어수가 같은데 전체 라인이 짧을경우 갱신
			minLen = lineLen;

		return;
	}
  	//가장 자리 코어일 경우,
	if (core[coreIdx].first == 0 || core[coreIdx].first == n - 1
		|| core[coreIdx].second == 0 || core[coreIdx].second == n - 1) {
		solution(map, coreIdx + 1, coreCnt + 1, lineLen);
		return;
	}
	
	bool flag = false;
	for (int i = 0; i < 4; i++) {
		int tmp[12][12];
		for (int e = 0; e < n; e++) {
			for (int r = 0; r < n; r++) {
				tmp[e][r] = map[e][r];
			} 
		} 
		int nx = core[coreIdx].first + dx[i];
		int ny = core[coreIdx].second + dy[i];
		int addLen = 0;
		while (tmp[nx][ny] == 0) { //power 연결 가능한가?
			if (nx == 0 || nx == n - 1 || ny == 0 || ny == n - 1) {
				addLen++;
				break;
			}
			nx += dx[i]; ny += dy[i];
			addLen++;
		}
		if ((nx == 0 || nx == n - 1 || ny == 0 || ny == n - 1) && addLen > 0 && tmp[nx][ny] == 0) { //만약 power 연결이 가능한 경우,
			int cx = core[coreIdx].first, cy = core[coreIdx].second;
			for (int j = 0; j < addLen; j++) {
				cx += dx[i];
				cy += dy[i];
				tmp[cx][cy] = 2;
			}
			solution(tmp, coreIdx + 1, coreCnt + 1, lineLen + addLen);
		}
		else {
			if(!flag)//이동 못하는 경우, 동일한 status로 한번 이상 돌리지 않는다.
			solution(tmp, coreIdx + 1, coreCnt, lineLen);
			flag = true;
		}
	}
}
void init() {
	minLen = 9999999;
	maxCnt = 0;
	core.clear();
}
int main() {
	int T;
	scanf("%d", &T);

	for (int tc = 0; tc < T; tc++) {
		init();
		scanf("%d", &n);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &a[i][j]);
				if (a[i][j] == 1) {
					core.push_back(make_pair(i, j));
				}
			}
		}
		solution(a, 0, 0, 0);
		printf("#%d %d\n",tc + 1, minLen);
	}
	
	return 0;
}
```

