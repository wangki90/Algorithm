```c++
// 규칙 + 시뮬레이션
// x,y 축 바뀜
#include <cstdio>
#include <algorithm>
#include <vector>
#include <utility>
#include <stack>
using namespace std;

typedef struct dcurve {
	int x;
	int y;
	int d;
	int g;
}dcurve;

vector<dcurve> v;
int map[101][101];
int n;
int dx[] = {1,0,-1,0};
int dy[] = {0,-1,0,1};
int answer;
void draw_map(dcurve cur) {

	int cx = cur.x;
	int cy = cur.y;
	int cdir = cur.d;
	int generation = cur.g;
	vector<int> cache;
	map[cy][cx] = 1;
	cache.push_back(cdir);
	while (generation > 0) { // cache에 저장된 마지막 방향부터 비교하며 다음 커브의 방향을 cache에 푸쉬.
		int csize = cache.size();
		for (int i = csize - 1; i >= 0; i--) {
			int ndir;
			cdir = cache[i];
			if (cdir == 0) {
				ndir = 1;
			}
			else if (cdir == 1) {
				ndir = 2;
			}
			else if (cdir == 2) {
				ndir = 3;
			}
			else {
				ndir = 0;
			}
			cache.push_back(ndir);
		}
		generation--;
	}
	//cache에 저장 된 방향 정보를 통해 map을 draw.
	for (int i = 0; i < cache.size(); i++) {
		int nx = cx + dx[cache[i]];
		int ny = cy + dy[cache[i]];
		cx = nx;
		cy = ny;
		map[ny][nx] = 1;
	}


}
int main() {

	answer = 0;
	for (int i = 0; i < 101; i++) {
		for (int j = 0; j < 101; j++) {
			map[i][j] = 0;
		}
	}
	scanf("%d",&n);

	for (int i = 0; i < n; i++) {
		dcurve tmp;
		scanf("%d %d %d %d", &tmp.x, &tmp.y, &tmp.d, &tmp.g);
		v.push_back(tmp);
	}
	for (int i = 0; i < n; i++) {
		draw_map(v[i]);
	}


	for (int i = 0; i < 100; i++) {
		for (int j = 0; j < 100; j++) {
			if (map[i][j] == 1 && map[i + 1][j] == 1 && map[i][j + 1] == 1 && map[i + 1][j + 1] == 1) {
				answer++;
			}
		}
	}


	printf("%d\n", answer);

	return 0;
}
```

