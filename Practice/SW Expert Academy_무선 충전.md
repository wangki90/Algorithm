```c++
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <vector>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
int map[11][11];
typedef struct BC {
	pair<int, int> locate;
	int c;
	int p;
}BC;
int m, a;
pair<int, int> person_A, person_B;
vector<BC> bc;
int move_A[101], move_B[101];
int dx[] = { 0,-1,0,1,0 };
int dy[] = { 0,0,1,0,-1 };
vector<int> tmp_A, tmp_B;
int answer;
void alloc_bc(BC cur_bc, int idx) {

	bool chk[11][11];
	for (int i = 0; i < 11; i++) {
		memset(chk[i], false, sizeof(chk[i]));
	}

	queue<pair<int, int>> que;
	que.push(make_pair(cur_bc.locate.first, cur_bc.locate.second));
	int loop = cur_bc.c;
	while (!que.empty()) {
		int queSize = que.size();
		for (int z = 0; z < queSize; z++) {
			int cx = que.front().first;
			int cy = que.front().second;
			que.pop();

			for (int i = 0; i < 5; i++) {
				int nx = cx + dx[i];
				int ny = cy + dy[i];

				if (nx < 0 || nx >= 10 || ny < 0 || ny >= 10)
					continue;
				if (chk[nx][ny])
					continue;

				chk[nx][ny] = true;
				que.push(make_pair(nx, ny));
				if (nx == person_A.first && ny == person_A.second) {
					tmp_A.push_back(idx);
				}
				if (nx == person_B.first && ny == person_B.second) {
					tmp_B.push_back(idx);
				}

			}
		}
		loop--;
		if (loop == 0)
			break;
	}
}
void selection() {

	if (tmp_A.size() > 0 && tmp_B.size() > 0) {
		if (tmp_A.size() == 1 && tmp_B.size() == 1 && tmp_A[0] == tmp_B[0]) {
			answer += bc[tmp_A[0]].p;
		}
		else if (tmp_A.size() == 1 && tmp_B.size() == 1 && tmp_A[0] != tmp_B[0]) {
			answer += (bc[tmp_A[0]].p + bc[tmp_B[0]].p);
		}
		else if (tmp_A.size() > 1 && tmp_B.size() > 1) {
			if (tmp_A[0] == tmp_B[0]) {
				if (bc[tmp_A[1]].p > bc[tmp_B[1]].p) {
					answer += (bc[tmp_B[0]].p + bc[tmp_A[1]].p);
				}
				else {
					answer += (bc[tmp_A[0]].p + bc[tmp_B[1]].p);
				}
			}
			else {
				answer += (bc[tmp_A[0]].p + bc[tmp_B[0]].p);
			}
		}
		else if (tmp_A.size() > 1 && tmp_B.size() == 1) {
			if (tmp_A[0] != tmp_B[0]) {
				answer += (bc[tmp_B[0]].p + bc[tmp_A[0]].p);
			}
			else {
				answer += bc[tmp_B[0]].p + bc[tmp_A[1]].p;
			}
		}
		else if (tmp_B.size() > 1 && tmp_A.size() == 1) {
			if (tmp_A[0] != tmp_B[0]) {
				answer += (bc[tmp_B[0]].p + bc[tmp_A[0]].p);
			}
			else {
				answer += bc[tmp_A[0]].p + bc[tmp_B[1]].p;
			}
		}

	}
	else if (tmp_A.size() > 0 && tmp_B.size() == 0) {
		answer += bc[tmp_A[0]].p;
	}
	else if (tmp_A.size() == 0 && tmp_B.size() > 0) {
		answer += bc[tmp_B[0]].p;
	}
	else if (tmp_A.size() == 0 && tmp_B.size() == 0) {
		answer += 0;
	}


}
bool compare(int a, int b) {
	return bc[a].p > bc[b].p;
}
int main() {
	int tc;
	cin >> tc;

	for (int test_case = 1; test_case <= tc; test_case++) {
		answer = 0;
		person_A = make_pair(0, 0);
		person_B = make_pair(9, 9);
		scanf("%d %d", &m, &a);
		move_A[0] = 0, move_B[0] = 0;
		memset(move_A, -1, sizeof(move_A));
		memset(move_B, -1, sizeof(move_B));

		for (int i = 1; i <= m; i++) {
			scanf("%d", &move_A[i]);
		}
		for (int i = 1; i <= m; i++) {
			scanf("%d", &move_B[i]);
		}
		bc.resize(a);
		for (int i = 0; i < a; i++) {
			scanf("%d %d %d %d", &bc[i].locate.second, &bc[i].locate.first, &bc[i].c, &bc[i].p);
			bc[i].locate.first -= 1; bc[i].locate.second -= 1;
		}

		for (int z = 0; z <= m; z++) {

			person_A.first += dx[move_A[z]];
			person_A.second += dy[move_A[z]];
			
			person_B.first += dx[move_B[z]];
			person_B.second += dy[move_B[z]];
			tmp_A.clear();
			tmp_B.clear();
			for (int i = 0; i < a; i++) {
				alloc_bc(bc[i], i);
			}
			sort(tmp_A.begin(), tmp_A.end(), compare);
			sort(tmp_B.begin(), tmp_B.end(), compare);

			//printf("A : ");
			//for (int i = 0; i < tmp_A.size(); i++) {
			//	printf("%d ", bc[tmp_A[i]].p);
			//}
			//printf("B : ");
			//for (int i = 0; i < tmp_B.size(); i++) {
			//	printf("%d ", bc[tmp_B[i]].p);
			//}
			//printf("\n");
			selection();
		}
		printf("#%d %d\n", test_case, answer);
	}


	return 0;
}

```

