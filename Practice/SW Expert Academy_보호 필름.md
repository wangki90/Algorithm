```c++
//dfs 완탐 + 백트래킹
//백트레킹의 경우 더 이상 탐색 안하게 할 수 있는 조건을 잘 생각해 보아야 함.
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>

#define MIN 987654321
using namespace std;

int film[13][20];
int d, w, k;
int answer;
bool chk(int f[13][20]) {

	for (int i = 0; i < w; i++) {
		int conti[13];
		for (int j = 0; j < d; j++) {
			conti[j] = f[j][i];
		}
		int tmp = 1, max_conti = 1;
		for (int j = 0; j < d - 1; j++) {
			if (conti[j] == conti[j + 1]) {
				tmp++;
			}
			else {
				tmp = 1;
			}
			max_conti = max(max_conti, tmp);
		}
		if (max_conti < k) {
			return false;
		}
	}
	return true;
}
void proc(int c_film[13][20], int drug_cnt, int cur_cell) {

	if (chk(c_film)) {
		answer = min(answer, drug_cnt);
		if (answer == 0)
			return;
	}

	if (drug_cnt >= answer || cur_cell >= d) {
		return;
	}
	int cc_film[13][20];
	for (int i = 0; i < d; i++) {
		memcpy(cc_film[i], c_film[i],	sizeof(int) * w);
	}
	//x
	proc(cc_film, drug_cnt, cur_cell + 1);
	//a
	for (int i = 0; i < w; i++) {
		cc_film[cur_cell][i] = 0;
	}
	proc(cc_film, drug_cnt + 1, cur_cell + 1);
	//b
	for (int i = 0; i < w; i++) {
		cc_film[cur_cell][i] = 1;
	}
	proc(cc_film, drug_cnt + 1, cur_cell + 1);
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("sample_input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		answer = MIN;
		scanf("%d %d %d", &d, &w, &k);

		for (int i = 0; i < d; i++) {
			for (int j = 0; j < w; j++) {
				scanf("%d", &film[i][j]);
			}
		}
		if (chk(film)) {
			answer = 0;
			printf("#%d %d\n",test_case, answer);
		}
		else {
			proc(film, 0, 0);
			printf("#%d %d\n",test_case, answer);
		}
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

