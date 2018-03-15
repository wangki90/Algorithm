```c++
//시뮬레이션
#include <iostream>
#include <cstdio>
#include <cstring>
#include <utility>
#include <algorithm>
#include <vector>

using namespace std;
int n, x;
int map[20][20];
int tmp[20];
bool solution() {

	int continum = 1; //연속 된 땅의 갯수

	for (int i = 0; i < n - 1; i++) {
		if (tmp[i] == tmp[i + 1]) {
			continum++;
		}
		else if (tmp[i] == tmp[i + 1] + 1) { // >
			for (int j = 0; j < x - 1; j++) {
				if (i + j + 1 >= n) return false;
				if (tmp[i + j + 1] == tmp[i + j + 2]) {
					if (j == x - 2) {
						continum = 0;
						i += x - 1;
					}
				}
				else {
					return false;
				}
			}
		}
		else if (tmp[i] + 1 == tmp[i + 1]) { // <
			if (continum >= x) {
				continum = 1;
			}
			else {
				return false;
			}
		}
		else { //높이 차 1이상
			return false;
		}
	}
	return true;
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		scanf("%d %d", &n, &x);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
			}
		}
		int cnt = 0;
		for (int i = 0; i < n; i++) { //가로
			for (int j = 0; j < n; j++) {
				tmp[j] = map[i][j];
			}
			if (solution()) cnt++;
		}
        
		for (int i = 0; i < n; i++) { //세로
			for (int j = 0; j < n; j++) {
				tmp[j] = map[j][i];
			}
			if (solution()) cnt++;
		}

		printf("#%d %d\n",test_case, cnt);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

