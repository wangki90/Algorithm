```c++
#include <iostream>
#include <cstdio>
#include <cstring>
#include <utility>
#include <algorithm>
#include <vector>

using namespace std;
int k;
int a[4][8];
vector<pair<int, int>> cmd;
void change_dir_r(int idx) {

	int tmp = a[idx][7];
	memmove(&a[idx][1], &a[idx][0], 7 * sizeof(int));
	a[idx][0] = tmp;
}
void change_dir_l(int idx) {

	int tmp = a[idx][0];
	memmove(&a[idx][0], &a[idx][1], 7 * sizeof(int));
	a[idx][7] = tmp;

}
void works(int idx, int dir) {

	int isRot[4] = { 0,0,0,0 };
	if (idx == 0) {
		isRot[0] = dir;
		if (a[0][2] != a[1][6]) {
			if (dir == 1) {
				isRot[1] = -1;
			}
			else {
				isRot[1] = 1;
			}
		}
		if (a[1][2] != a[2][6]) {
			if (isRot[1] == 1) {
				isRot[2] = -1;
			}
			else if (isRot[1] == -1) {
				isRot[2] = 1;
			}
		}
		if (a[2][2] != a[3][6]) {
			if (isRot[2] == 1) {
				isRot[3] = -1;
			}
			else if (isRot[2] == -1) {
				isRot[3] = 1;
			}
		}
	}
	else if (idx == 1) {
		isRot[1] = dir;
		if (a[1][6] != a[0][2]) {
			if (isRot[1] == 1) {
				isRot[0] = -1;
			}
			else if (isRot[1] == -1) {
				isRot[0] = 1;
			}
		}
		if (a[1][2] != a[2][6]) {
			if (isRot[1] == 1) {
				isRot[2] = -1;
			}
			else if (isRot[1] == -1) {
				isRot[2] = 1;
			}
		}
		if (a[2][2] != a[3][6]) {
			if (isRot[2] == 1) {
				isRot[3] = -1;
			}
			else if (isRot[2] == -1) {
				isRot[3] = 1;
			}
		}
	}
	else if (idx == 2) {
		isRot[2] = dir;
		if (a[2][2] != a[3][6]) {
			if (isRot[2] == 1) {
				isRot[3] = -1;
			}
			else if (isRot[2] == -1) {
				isRot[3] = 1;
			}
		}
		if (a[2][6] != a[1][2]) {
			if (isRot[2] == 1) {
				isRot[1] = -1;
			}
			else if (isRot[2] == -1) {
				isRot[1] = 1;
			}
		}
		if (a[1][6] != a[0][2]) {
			if (isRot[1] == 1) {
				isRot[0] = -1;
			}
			else if (isRot[1] == -1) {
				isRot[0] = 1;
			}
		}
	}
	else {
		isRot[3] = dir;
		if (a[3][6] != a[2][2]) {
			if (isRot[3] == 1) {
				isRot[2] = -1;
			}
			else if (isRot[3] == -1) {
				isRot[2] = 1;
			}
		}
		if (a[2][6] != a[1][2]) {
			if (isRot[2] == 1) {
				isRot[1] = -1;
			}
			else if (isRot[2] == -1) {
				isRot[1] = 1;
			}
		}
		if (a[1][6] != a[0][2]) {
			if (isRot[1] == 1) {
				isRot[0] = -1;
			}
			else if (isRot[1] == -1) {
				isRot[0] = 1;
			}
		}
	}

	for (int i = 0; i < 4; i++) {
		if (isRot[i] != 0) {
			if (isRot[i] == 1) {
				change_dir_r(i);
			}
			else {
				change_dir_l(i);
			}
		}
	}

}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		cmd.clear();
		scanf("%d", &k);
		for (int i = 0; i < 4; i++) {
			for (int j = 0; j < 8; j++) {
				scanf("%d", &a[i][j]);
			}
		}
		for (int i = 0; i < k; i++) {
			int x, y;
			scanf("%d %d", &x, &y);
			x--;
			cmd.push_back(make_pair(x,y));
		}
		for (int i = 0; i < k; i++) {
			works(cmd[i].first,cmd[i].second);
		}
		
		int sum = 0;

		for (int i = 0; i < 4; i++) {
			if (a[i][0] == 1) {
				sum += pow(2, i);
			}
		}
		printf("#%d %d\n",test_case, sum);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

