```c++
/*
완탐 + 중복 제거
char arr --> char arr 복사 : strcpy(out,in)
string --> char arr 복사 : strcpy(cstr, str.c_str())
char arr --> string : string str = cstr
string 길이 --> str.length()
char arr --> int : num = atoi(cstr)
string --> int : intValue = atoi(str.c_str())
int --> string : str = to_string(intValue)
*/
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <string>
#include <cstring>
using namespace std;
char in[6];
int answer;
int cnt;
int k;
bool chk[100][1000000];
void solution(char out[6], int depth, int end) {

	if (depth == end) {
		int num = atoi(out);
		answer = max(answer, num);
		return;
	}
	
	for (int i = 0; i < cnt - 1; i++) {
		for (int j = i + 1; j < cnt; j++) {
			swap(out[i], out[j]);
			int tmp = atoi(out);
			if (!chk[depth][tmp]) {
				chk[depth][tmp] = true;
				solution(out, depth + 1, end);
			}
			swap(out[i], out[j]);
		}
	}

}
int main() {
	int T;

	cin >> T;

	for (int tc = 1; tc <= T; tc++) {
		for (int i = 0; i < 7; i++) {
			memset(chk[i], false, sizeof(chk[i]));
		}
		answer = 0;
		int k;
		string num;
		cin >> num;
		cin >> k;
		cnt = num.length();
		strcpy(in, num.c_str());
		solution(in, 0, k);
		printf("#%d %d\n", tc, answer);
	}


	return 0;
}
```

