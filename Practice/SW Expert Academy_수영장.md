```c++
//dfs, 완전탐색
#include <cstdio>
#include <algorithm>
#include <vector>

using namespace std;
vector<int> fee;
vector<int> schedule;
int answer = 99999999;
vector<int> result;
void dfs(int cost, int month, int flag) {

	if (month == 12) {
		answer = min(answer, cost);
		return;
	}
	//전 노드가 세 달이 아닐 경우,
	if (flag == 0) {
		//하루
		dfs(cost + (schedule[month] * fee[0]), month + 1, 0);
		//한 달
		dfs(cost + fee[1], month + 1, 0);
		//세 달 
		dfs(cost + fee[2], month + 1, flag + 1);
	}
    //전 노드가 세 달인 경우,
	else { 
		if (flag == 2)
			dfs(cost, month + 1, 0);
		else
			dfs(cost, month + 1, flag + 1);
	}

}
int main() {
	int T;
	scanf("%d", &T);

	for (int test = 0; test < T; test++) {
		answer = 99999999;
		fee.clear();
		schedule.clear();
		for (int i = 0; i < 4; i++) {
			int x;
			scanf("%d", &x);
			fee.push_back(x);
		}
		for (int i = 0; i < 12; i++) {
			int x;
			scanf("%d", &x);
			schedule.push_back(x);
		}

		dfs(0,0,0);
		answer = min(answer, fee[3]);
		result.push_back(answer);
	}
	for (int i = 0; i < result.size(); i++) {
		printf("#%d %d\n", i + 1, result[i]);
	}
	return 0;
}
```

