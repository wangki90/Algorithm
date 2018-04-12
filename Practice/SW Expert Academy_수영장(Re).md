```c++
//REVIEW
#include <iostream>
#include <cstdio>
#include <algorithm>
#define MIN 987654321

using namespace std;
int price[4];
int plan[12];
int answer;

void dfs(int depth, int total_price, int is3mon) {


	if (depth == 12) {
		answer = min(total_price, answer);
		return;
	}
	if (is3mon == 3) {
		is3mon = 0;
	}
	if (is3mon > 0 && is3mon < 3) {
		dfs(depth + 1, total_price, is3mon + 1);
	}
	else {
		dfs(depth + 1, total_price + (price[0] * plan[depth]), is3mon); //1day
		dfs(depth + 1, total_price + price[1], is3mon); //1month
		dfs(depth + 1, total_price + price[2], is3mon + 1); //3month
	}
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		answer = MIN;
		for (int i = 0; i < 4; i++) {
			scanf("%d", &price[i]);
		}
		for (int i = 0; i < 12; i++) {
			scanf("%d", &plan[i]);
		}

		dfs(0, 0, 0);

		answer = min(price[3], answer);
		printf("#%d %d\n", test_case, answer);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

