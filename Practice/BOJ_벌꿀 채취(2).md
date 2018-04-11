```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <utility>
#include <vector>
#include <cmath>
using namespace std;

int n, m, c;
int a[11][11];
int max_value;
int tmp,tmp2;
int tmp_x, tmp_y;
void cal(int total, int square, int depth) {

	if (total > c) {
		return;
	}

	if (depth == m ) {
		tmp = max(tmp, square);
		return;
	}

	cal(total, square, depth + 1);//채취 안하거나
	cal(total + a[tmp_x][tmp_y + depth], square + pow(a[tmp_x][tmp_y + depth], 2), depth + 1); //채취 하거나
}
void selection(pair<int, int> first, pair<int, int> second) {

	int a_ = 0, b_ = 0;
	tmp = 0; tmp_x = first.first; tmp_y = first.second;
	cal(0, 0 ,0);
	a_ = tmp;
	tmp = 0;
	tmp_x = second.first; tmp_y = second.second;
	cal(0, 0, 0);
	b_ = tmp;
	//printf("%d %d\n", a_, b_);
	max_value = max(max_value, a_ + b_);


}
int main(int argc, char** argv)
{

	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		max_value = 0;
		tmp = 0;
		scanf("%d %d %d", &n, &m, &c);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &a[i][j]);
			}
		}
		pair<int, int> s1, s2;
		//두사람이 채취할 수 있는 벌꿀의 각각 시작 좌표
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				s1.first = i; s1.second = j;
				if (j + (m - 1) >= n)
					break;

				for (int k = i; k < n; k++) {
					if (i == k) {
						for (int l = j + m; l < n; l++) {
							s2.first = k; s2.second = l;
							if (l + (m - 1) >= n)
								break;

							selection(s1, s2);
						}
					}
					else {
						for (int l = 0; l < n; l++) {
							s2.first = k; s2.second = l;
							if (l + (m - 1) >= n)
								break;

							selection(s1, s2);
						}
					}

				}
			}
		}

		printf("#%d %d\n", test_case, max_value);


	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

