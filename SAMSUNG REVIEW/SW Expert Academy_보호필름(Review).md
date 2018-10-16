```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <utility>
#include <vector>
#include <cstring>
#define MAX 9999999
using namespace std;
int d, w, k;
int map[14][21];
int answer;
bool isPass() {

	bool flag = true;
	for (int i = 0; i < w; i++) {
		int cnt = 1;
		int cur = map[0][i];
		int max_cnt = 1;
		for (int j = 1; j < d; j++) {
			int next = map[j][i];
			if (cur == next) {
				cur = next;
				cnt++;
				max_cnt = max(max_cnt, cnt);
			}
			else {
				cur = next;
				cnt = 1;
			}
		}
		if (max_cnt < k) {
			flag = false;
			break;
		}
	}

	return flag;

}
void solution(int depth, int drug_cnt) {


	if (isPass()) {
		answer = min(answer, drug_cnt);
	}

	if (answer <= drug_cnt)
		return;

	if (depth == d) {
		return;
	}

	int copy_map[21];
	for (int i = 0; i < w; i++) {
		copy_map[i] = map[depth][i];
	}



	solution(depth + 1, drug_cnt);
	
	for (int i = 0; i < w; i++) {
		map[depth][i] = 0;
	}
	solution(depth + 1, drug_cnt + 1);


	for (int i = 0; i < w; i++) {
		map[depth][i] = 1;
	}
	solution(depth + 1, drug_cnt + 1);
	for (int i = 0; i < w; i++) {
		map[depth][i] = copy_map[i];
	}

}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("C:/Users/Wang Kyu Bong/Desktop/sample_input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		answer = MAX;

		scanf("%d %d %d", &d, &w, &k);

		for (int i = 0; i < d; i++) {
			for (int j = 0; j < w; j++) {
				scanf("%d", &map[i][j]);
			}
		}


		if (isPass()) {
			printf("#%d %d\n", test_case, 0);
		}
		else {
			solution(0, 0);//depth, 약품, 약품 처리 개수
			printf("#%d %d\n", test_case, answer);
		}

	}
	return 0;
}
```

