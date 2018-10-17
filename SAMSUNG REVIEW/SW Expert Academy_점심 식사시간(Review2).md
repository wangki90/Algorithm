```c++
//의식 흐름대로 짬
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <vector>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
#define MAX 9999999
using namespace std;
typedef struct stair {
	int x;
	int y;
	int length;
}stair;
int n;
int map[11][11];
vector<stair> str;
vector<pair<int, int>> person;
int select_stair[11];
int answer;
void get_time() {

	int arrival_time[11];

	for (int i = 0; i < person.size(); i++) {

		arrival_time[i] = abs(str[select_stair[i]].x - person[i].first) + abs(str[select_stair[i]].y - person[i].second);
	}

	queue<int> que[2];
	int end_time[11];
	int time = 1;
	bool chk[11];
	for (int i = 0; i < 11; i++) {
		end_time[i] = -1;
		chk[i] = false;
	}
	while (1) {
		//계단 완료 사람 제거
		for (int i = 0; i < person.size(); i++) {

			if (chk[i])
				continue;

			int arv_time = arrival_time[i];
			int sel_stair = select_stair[i];

			if (time >= end_time[i] && end_time[i] != -1 && !chk[i]) {
				que[sel_stair].pop();
				chk[i] = true;
			}
		}
		//계단 이동
		for (int i = 0; i < person.size(); i++) {

			if (chk[i])
				continue;

			int arv_time = arrival_time[i];
			int sel_stair = select_stair[i];


			if (arv_time <= time && que[sel_stair].size() < 3 && !chk[i] && end_time[i] == -1) {
				if (arv_time == time) {
					que[sel_stair].push(i);
					end_time[i] = time + str[sel_stair].length + 1;
				}
				else if (arv_time < time) {
					que[sel_stair].push(i);
					end_time[i] = time + str[sel_stair].length;
				}
			}
		}
		bool flag = true;
		for (int i = 0; i < person.size(); i++) {
			if (!chk[i]) {
				flag = false;
				break;
			}
		}

		if (flag) {
			answer = min(answer, time);
			return;
		}

		time += 1;
	}

}
void selection(int depth) {

	if (depth == person.size()) {

		get_time();
		return;
	}

	for (int i = 0; i < 2; i++) {
		select_stair[depth] = i;
		selection(depth + 1);
	}
}
void init() {
	answer = MAX;
	person.clear();
	str.clear();
}
int main() {

	int T;
	cin >> T;
	for (int test_case = 1; test_case <= T; test_case++) {
		init();
		scanf("%d", &n);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
				if (map[i][j] == 1) {
					person.push_back(make_pair(i, j));
				}
				else if (map[i][j] > 1) {
					stair tmp;
					tmp.x = i;
					tmp.y = j;
					tmp.length = map[i][j];
					str.push_back(tmp);
				}
			}
		}
		selection(0);

		printf("#%d %d\n", test_case, answer);

	}

}
```

