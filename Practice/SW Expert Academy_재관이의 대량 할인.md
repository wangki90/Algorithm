```c++
#include <iostream>
#include <cstring>
#include <algorithm>
#include <functional>
using namespace std;

int n;
int price[100000];

int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		scanf("%d", &n);

		for (int i = 0; i < n; i++) {
			scanf("%d", &price[i]);
		}
		sort(price, price + n, greater<int>());
		int total_price = 0;
		for (int i = 0; i < n; i++) {
			if ((i + 1) % 3 == 0)continue;
			else {
				total_price += price[i];
			}
		}

		printf("#%d %d\n", test_case, total_price);
	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

