```c++
//DFS 길찾기
#include <cstdio>
#include <utility>
#include <cstring>
using namespace std;

int a[16][16];
bool chk[16][16];
int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };
pair<int, int> start, end_;
bool flag = false;
void solution(int x,int y) {

	if (x == end_.first && y == end_.second) {
		flag = true;
		return;
	}

	chk[x][y] = true;

	for (int i = 0; i < 4; i++) {
		int nx = x + dx[i];
		int ny = y + dy[i];
		if((a[nx][ny] == 0 || a[nx][ny] == 3) && !chk[nx][ny])
			solution(nx, ny);
	}
}
int main() {

	for (int t = 0; t < 10; t++) {
		int tc;
		scanf("%d", &tc);
		flag = false;
		for (int i = 0; i < 16; i++) {
			for (int j = 0; j < 16; j++) {
				scanf("%1d", &a[i][j]);
				if (a[i][j] == 2)
					start = make_pair(i, j);
				else if (a[i][j] == 3)
					end_ = make_pair(i, j);
			}
		}

		solution(start.first, start.second);

		if(flag)
			printf("#%d 1\n", tc);
		else
			printf("#%d 0\n", tc);

		for (int i = 0; i < 16; i++)
			memset(chk[i], false, sizeof(chk[i]));
	}
	return 0;
}
```

