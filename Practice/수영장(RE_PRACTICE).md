```c++
//dfs 완전 탐색 기본문제.
//SW Expert Academy 수영장 복습.
#include <cstdio>
#include <algorithm>


using namespace std;
int month[12];
int price[4];
int total_price;

void dfs(int depth, int total, int isQuarter, int isYear) {

	if (depth == 12 || isYear) {
		total_price = min(total_price, total);
		return;
	}
	if (isQuarter > 0 && isQuarter < 3) {
		if (isQuarter == 2)
			dfs(depth + 1, total, 0, isYear);
		else
			dfs(depth + 1, total, isQuarter + 1, isYear);
	}
	else {
		dfs(depth + 1, total + month[depth] * price[0], 0, 0); //1일권
		dfs(depth + 1, total + price[1], 0, 0); //한달권
		dfs(depth + 1, total + price[2], isQuarter + 1, 0); //세달권
		dfs(depth + 1, total + price[3], 0, 1); //일년권
	}
}
int main() {

	int T;
	scanf("%d", &T);

	for (int tc = 0; tc < T; tc++) {
		total_price = 987654321;
		for (int i = 0; i < 4; i++) {
			scanf("%d", &price[i]);
		}
		for (int i = 0; i < 12; i++) {
			scanf("%d", &month[i]);
		}
		dfs(0,0,0,0);
		printf("#%d %d\n", tc + 1, total_price);
	}

	return 0;
}
```

