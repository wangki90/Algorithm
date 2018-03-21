```c++
#include<iostream>
#include <cstring>
#include <string>
using namespace std;
int a[4][14];
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		string cmd;
		bool flag = false;
		memset(a, 0, sizeof(a));

		cin >> cmd;

		for (int i = 0; i < cmd.length(); i += 3) {
			int t, x = 1;
			for (int j = i; j < i + 3; j++) {
				if (j == i) {
					if (cmd[j] == 'S') {
						t = 0;
					}
					else if (cmd[j] == 'D') {
						t = 1;
					}
					else if (cmd[j] == 'H') {
						t = 2;
					}
					else {
						t = 3;
					}
				}
				else if (j == i + 1) {
					if (cmd[j] - '0' == 1) {
						x *= 10;
					}
					else {
						x = 0;
					}
				}
				else {
					x += (cmd[j] - '0');
				}
			}
			if (a[t][x] == 0) {
				a[t][x] = 1;
			}
			else {
				flag = true;
				break;
			}
		}

		if (flag) {
			printf("#%d ERROR\n",test_case);
		}
		else {
			int s = 0, d = 0, h = 0, c = 0;
			for (int i = 1; i < 14; i++) {
				if (a[0][i] == 0) s++;
				if (a[1][i] == 0) d++;
				if (a[2][i] == 0) h++;
				if (a[3][i] == 0) c++;
			}
			printf("#%d %d %d %d %d\n",test_case, s, d, h, c);
		}

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

