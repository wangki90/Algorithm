```c++
//여러개 중에서 큰 애만 살아남는 부분 구현방식 Review하기.
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <queue>
#include <utility>
#include <vector>
#include <cstring>

using namespace std;

typedef struct cell{
	int x;
	int y;
	int life;
	int time;
}cell;
int n, m, k;
int map[1001][1001];
bool chk[1001][1001];
int dx[] = { 1,0,-1,0 };
int dy[] = { 0,1,0,-1 };
int main() {

	int tc;
	cin >> tc;

	for (int test_case = 1; test_case <= tc; test_case++) {
		
		queue<cell> que;
		for (int i = 0; i < 1001; i++) {
			memset(chk[i], false, sizeof(chk[i]));
			memset(map[i], 0, sizeof(map[i]));
		}
		scanf("%d %d %d", &n, &m, &k);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < m; j++) {
				scanf("%d", &map[500 - (n / 2) + i][500 - (m / 2) + j]); // 중앙 배치
				if (map[500 - (n / 2) + i][500 - (m / 2) + j] == 0)
					continue;
				cell tmp;
				tmp.x = 500 - (n / 2) + i;
				tmp.y = 500 - (m / 2) + j;
				tmp.life = map[500 - (n / 2) + i][500 - (m / 2) + j];
				tmp.time = 2 * tmp.life;
				que.push(tmp);
				chk[tmp.x][tmp.y] = true;
				map[tmp.x][tmp.y] = tmp.life;
			}
		}
	
		while (k > 0) {

			int queSize = que.size();
			queue<cell> tmp_que;
			for (int z = 0; z < queSize; z++) {
				cell tmp = que.front();
				int cx = que.front().x;
				int cy = que.front().y;
				int life = que.front().life;
				int time = que.front().time;

				que.pop();


				if (time > life) { //비활성
					tmp.time--;
					que.push(tmp);
				}
				else if (time == life) { //최초 활성
					tmp.time--;
					//다음턴에도 살아있는것만 push
					if(tmp.time != 0)
						que.push(tmp);
					for (int i = 0; i < 4; i++) {
						int nx = cx + dx[i];
						int ny = cy + dy[i];

						if (chk[nx][ny])
							continue;
						
						if (map[nx][ny] < life) {
							cell tmp2;
							tmp2.x = nx;
							tmp2.y = ny;
							tmp2.life = life;
							tmp2.time = 2 * life;
							map[nx][ny] = life;
							tmp_que.push(tmp2);
						}
					}
				}
				else if(time > 0 && time < life){ //활성
					tmp.time--;
					//다음턴에도 살아있는것만 push
					if(tmp.time != 0)
						que.push(tmp);
				}
			}
			k--;
			// 가장 큰 생명력 수치를 가진것만 다음으로.
			queSize = tmp_que.size();
			for (int i = 0; i < queSize; i++) {
				cell tmp = tmp_que.front();
				tmp_que.pop();
				if (map[tmp.x][tmp.y] == tmp.life) {
					que.push(tmp);
					chk[tmp.x][tmp.y] = true;
				}
			}


		}

		printf("#%d %d\n",test_case, que.size());

	}
	return 0;
}


```

