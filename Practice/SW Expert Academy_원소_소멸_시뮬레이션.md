```c++
//STL 큐 사용 -> 시간초과
//배열로 큐 구현
//vector<pair<pair<int, int>, pair<int, int> >> 사용 -> 시간초과
//pair<pair<int, int>, pair<int, int> > -> 구조체로 구현
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <queue>
#include <utility>
#include <vector>
#include <cstring>
#define MAX 1001
using namespace std;
typedef struct atm {
	int x;
	int y;
	int dir;
	int k;

}atm;
int map[4001][4001];
int n;
vector<atm> atom; // x, y, 방향, 에너지
int dx[] = { 0, 0, -1, 1}; // y값 증가방향, y값 감소방향, x값 증가방향, x값 감소방향
int dy[] = { 1, -1, -0, 0};
int answer;


atm q[MAX];
int front = 0;
int rear = 0;
int qsize = 0;
bool empty()
{
	if (front == rear)
		return true;
	else
		return false;
}


void push(atm tmp)
{
	qsize++;
	q[rear] = tmp;
	rear = (rear + 1) % MAX;
}

atm pop()
{
	atm ret;
	qsize--;
	ret = q[front];
	front = (front + 1) % MAX;
	return ret;
}

void init() {

	for (int i = 0; i < n; i++) {
		int x = atom[i].x;
		int y = atom[i].y;
		map[x][y] = atom[i].k;
	}
}

void solution() {
	
	init();

	//queue<atm> que;

	for (int i = 0; i < n; i++) {
		push(atom[i]);
	}

	
	while (!empty()) {
		int queSize = qsize;
		vector<pair<int, int>> spot;
		for (int z = 0; z < queSize; z++) {
			atm tmp2 = pop();
			int cx = tmp2.x;
			int cy = tmp2.y;
			int nx = cx + dx[tmp2.dir];
			int ny = cy + dy[tmp2.dir];
			int cdir = tmp2.dir;
			int ck = tmp2.k;

			//que.pop();

			//충돌한 원소인데 큐에 들어간 경우, 좌표값은 0으로 초기화 되어 있음
			if (map[cx][cy] < ck) {
				answer += ck;
				continue;
			}

			//범위 밖의 원소
			if (nx < 0 || nx >= 4001 || ny < 0 || ny >= 4001) {
				map[cx][cy] = 0;
				continue;
			}

			//충돌 지점
			if (map[nx][ny] > 0) {
				map[nx][ny] += ck;
				map[cx][cy] = 0;
				answer += ck;
				spot.push_back(make_pair(nx, ny)); // 충돌 좌표 저장
				continue;
			}
			//충돌 x
			else {
				map[nx][ny] = ck;
				map[cx][cy] = 0;
				atm tmp;
				tmp.x = nx; tmp.y = ny; tmp.dir = cdir; tmp.k = ck;
				push(tmp);
			}
		}
		// 충돌지점 0으로 바꿈
		for (int i = 0; i < spot.size(); i++) {
			map[spot[i].first][spot[i].second] = 0;
		}
		spot.clear();
	}
}
int main() {

	int tc;

	cin >> tc;

	for (int test_case = 1; test_case <= tc; test_case++) {
		atom.clear();
		answer = 0;
		scanf("%d", &n);

		for (int i = 0; i < n; i++) {

			int x, y, dir, k;
			atm tmp;
			scanf("%d %d %d %d", &y, &x, &dir, &k);

			y += 1000;
			x += 1000;
			tmp.x = 2 * y; tmp.y = 2 * x; tmp.dir = dir; tmp.k = k;
			atom.push_back(tmp);

		}


		solution();
		printf("#%d %d\n",test_case, answer);

	}
	return 0;
}
```

