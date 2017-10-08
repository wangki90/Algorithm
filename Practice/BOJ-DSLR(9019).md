```c++
//BFS,완전탐색
#include <vector>
#include <cstdio>
#include <algorithm>
#include <queue>
#include <cstring>
#include <iostream>
#include <string>
using namespace std;

int init;
int result;
bool chk[10001];
int parent[10001];
char cmd[10001];
char c[] = { 'D','S','L','R' };
vector<vector<char>> answer;
int multiple(int x){
	return (2 * x) % 10000;
}
int sub(int x){
	return (x + 9999) % 10000;
}
int left(int x){
	if (x == 0)return 0;
	int left = x / 1000;
	int right = x % 1000;
	return right * 10 + left;
}
int right(int x){
	if (x == 0)return 0;
	int left = x / 10;
	int right = x % 10;
	return right * 1000 + left;
}
void bfs() {
	
	memset(chk, false, sizeof(chk));
	memset(parent, 0, sizeof(parent));
	memset(cmd, '0', sizeof(cmd));

	queue<int> que;
	que.push(init);
	chk[init] = true;

	int tmp[4];

	while (!que.empty() && que.front() != result) {
		int cx = que.front();
		que.pop();
		tmp[0] = multiple(cx);
		tmp[1] = sub(cx);
		tmp[2] = left(cx);
		tmp[3] = right(cx);
		for (int i = 0; i < 4; i++) {
			if (!chk[tmp[i]]) {
				que.push(tmp[i]);
				chk[tmp[i]] = true;
				cmd[tmp[i]] = c[i];
				parent[tmp[i]] = cx;
			}
		}
	}
}
int main() {
	int T;
	scanf("%d", &T);
	for (int test = 0; test < T; test++) {
		scanf("%d %d", &init, &result);
		
		bfs();

		string str;

		while (init != result) {
			str.push_back(cmd[result]);
			result = parent[result];
		}
		reverse(str.begin(), str.end());
		cout << str << endl;
	}

	return 0;
}
```

