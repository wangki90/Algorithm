```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
#include <queue>
using namespace std;

int n;
int map[10][10];
int visit[10][10][10];
vector<pair<int, int>> person, stair;
int select_stair[10];
int answer;
void find_time() {

	int time = 0;
	int chk[10];
	int arrivalTime[10];

	for (int i = 0; i < person.size(); i++) {
		arrivalTime[i] = abs(person[i].first - stair[select_stair[i]].first) + abs(person[i].second - stair[select_stair[i]].second);
		chk[i] = 0;
	}

	queue < pair<int, int>> q1, q2;

	while (1) {

		time++;

		while (!q1.empty()) {
			if (q1.front().second <= time) {
				q1.pop();
			}
			else {
				break;
			}
		}

		while (!q2.empty()) {
			if (q2.front().second <= time) {
				q2.pop();
			}
			else {
				break;
			}
		}

		for (int i = 0; i < person.size(); i++) {
			int qs1 = q1.size(); int qs2 = q2.size();

			if (time >= arrivalTime[i] && qs1 < 3 && select_stair[i] == 0 && chk[i] == 0) {
				int endTime;
				if (arrivalTime[i] == time) {
					endTime = time + map[stair[0].first][stair[0].second] + 1;
				}
				else {
					endTime = time + map[stair[0].first][stair[0].second];
				}
				q1.push(make_pair(i, endTime));
				chk[i] = 1;
			}
			if (time >= arrivalTime[i] && qs2 < 3 && select_stair[i] == 1 && chk[i] == 0) {
				int endTime;
				if (arrivalTime[i] == time) {
					endTime = time + map[stair[1].first][stair[1].second] + 1;
				}
				else {
					endTime = time + map[stair[1].first][stair[1].second];
				}
				q2.push(make_pair(i, endTime));
				chk[i] = 1;
			}
		}

		int tmp = 0;

		for (int i = 0; i < person.size(); i++) {
			if (chk[i] == 1) {
				tmp++;
			}
			else {
				break;
			}
		}
		if (tmp == person.size() && q1.empty() && q2.empty()) {
			answer = min(answer, time);
			return;
		}

	}




}

void stair_select(int depth, int cur) {

	if (depth == person.size()) {
		find_time();
		return;
	}

	select_stair[depth] = 0;
	stair_select(depth + 1, cur + 1);
	select_stair[depth] = 1;
	stair_select(depth + 1, cur + 1);

}

int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		answer = 987654321;
		person.clear();
		stair.clear();
		scanf("%d", &n);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
				if (map[i][j] == 1)
					person.push_back(make_pair(i, j));
				else if (map[i][j] > 1)
					stair.push_back(make_pair(i, j));
			}
		}

		stair_select(0,0);

		printf("#%d %d\n",test_case,answer);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

