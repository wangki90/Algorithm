```c++
//dfs 완탐 + 백트래킹
//백트레킹의 경우 더 이상 탐색 안하게 할 수 있는 조건을 잘 생각해 보아야 함.
#include <cstdio>
#include <algorithm>

using namespace std;

int D, W, K;
int film[13][20];
int maxNum[20][1];
int answer;
bool check(int F[13][20]) {
	for (int i = 0; i < W; i++) {
		int count = 1;
		int maxCnt = 0;
		int cur, prev = F[0][i];
		for (int j = 1; j < D; j++) {
			cur = F[j][i];
			if (cur == prev) {
				count++;
			}
			else {
				count = 1;
			}
			maxCnt = max(maxCnt, count);
			prev = cur;
		}
		if (maxCnt < K) return false;
		maxNum[i][0] = maxCnt;
	}
	return true;
}
int solution(int Fm[13][20], int drugNum, int depth) {

	if (drugNum >= answer) {
		return answer;
	}

	if (check(Fm)) {
		answer = min(answer, drugNum);
		if (answer == 0)
			return answer;
	}
	if (depth == D) {
		return answer;
	}
	
	int tmp[13][20];
	for (int i = 0; i < D; i++) {
		for (int j = 0; j < W; j++) {
			tmp[i][j] = Fm[i][j];
		}
	}

	solution(tmp, drugNum, depth + 1);

	for (int i = 0; i < W; i++) {
		tmp[depth][i] = 0;
	}
	solution(tmp, drugNum + 1, depth + 1);

	for (int i = 0; i < W; i++) {
		tmp[depth][i] = 1;
	}
	solution(tmp, drugNum + 1, depth + 1);

}
int main() {

	int T;
	scanf("%d", &T);

	for (int tc = 0; tc < T; tc++) {
		answer = 99;
		scanf("%d %d %d", &D, &W, &K);

		for (int i = 0; i < D; i++) {
			for (int j = 0; j < W; j++) {
				scanf("%d", &film[i][j]);
			}
		}

		answer = solution(film, 0, 1);

		for (int i = 0; i < W; i++) {
			film[0][i] = 0;
		}
		answer = solution(film, 1, 1);

		for (int i = 0; i < W; i++) {
			film[0][i] = 1;
		}
		answer = solution(film, 1, 1);

		printf("#%d %d\n", tc + 1, answer);
	}
	return 0;
}

```

