```c++
//이상한 피라미드 체험
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;

int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		int a, b, answer = 0;
		scanf("%d %d", &a, &b);
		if (a > b) {
			int tmp = a;
			a = b;
			b = tmp;
		}

		int cell_a, cell_b;
		int padding_a, padding_b;
		int n = 1;

		while (n*(n + 1) / 2 < a) {
			n++;
		}
		cell_a = n; 
		padding_a = (n*(n + 1) / 2) - a;
		n = 1;
		while (n*(n + 1) / 2 < b) {
			n++;
		}
		cell_b = n;
		padding_b = (n*(n + 1) / 2) - b;
		int dist = abs(cell_b - cell_a);
		if (padding_b >= padding_a && padding_b <= padding_a + dist) {
			answer = dist;
		}
		else if (padding_b < padding_a) {
			answer = dist + padding_a - padding_b;
		}
		else if (padding_b > padding_a + dist) {
			answer = dist + padding_b - (padding_a + dist);
		}
		
		printf("#%d %d\n", test_case, answer);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

