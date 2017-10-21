```c++
#include <cstdio>
#include <vector>
#include <algorithm>
#include <queue>

using namespace std;
int map[11][11];
int n;
vector<pair<int, int> > person;
vector<pair<int, int> > stair;
int selectStair[11];
int cnt = 0;
int answer;
void solution(int selectStair[11]) {

	int time = 0;
	vector<bool> chk(person.size());
	vector<int> arrivalTime(person.size());
	
	//각 사람마다 도착시간 저장
	for (int i = 0; i < person.size(); i++) {
		arrivalTime[i] = abs(person[i].first - stair[selectStair[i]].first) + abs(person[i].second - stair[selectStair[i]].second);
	}
	queue<pair<int, int> > sq1;
	queue<pair<int, int> > sq2;
	while (1) {

		time++;
		//계단1 끝
		while (!sq1.empty()) {
			if (sq1.front().second <= time)
				sq1.pop();
			else 
				break;
		}
		//계단2 끝
		while (!sq2.empty()) {
			if (sq2.front().second <= time)
				sq2.pop();
			else
				break;
		}
		//각 사람마다 시간에 맞게 계단 입장, 3명 이상일때 대기, 도착 시간보다 늦은 시간에 입장할 경우 +1 하지 않고 바로 입장
		for (int i = 0; i < person.size(); i++) {
			int qs1 = sq1.size(), qs2 = sq2.size();
			int t = arrivalTime[i];
			if (time >= arrivalTime[i] && qs1 < 3 && selectStair[i] == 0 && !chk[i]) {
				sq1.push(make_pair(i, (t = arrivalTime[i] < time ? time : arrivalTime[i] + 1) + map[stair[0].first][stair[0].second]));
				chk[i] = true;
			}
			if (time >= arrivalTime[i] && qs2 < 3 && selectStair[i] == 1 && !chk[i]) {
				sq2.push(make_pair(i, (t = arrivalTime[i] < time ? time : arrivalTime[i] + 1) + map[stair[1].first][stair[1].second]));
				chk[i] = true;
			}
		}

		//모든 사람 끝일경우 종료,
		int tmp = 0;
		for (int i = 0; i < person.size(); i++) {
			if (chk[i])tmp++;
			if (tmp == person.size() && sq1.empty() && sq2.empty()) {
				answer = min(answer, time);
				return;
			}
		}
	}
}
void dfs(int depth, int cur) {
	//dfs 모든 경우 탐색
	if (depth == person.size()) {
		solution(selectStair);
		return;
	}
	
	selectStair[cur] = 0;
	dfs(depth + 1, cur + 1);
	selectStair[cur] = 1;
	dfs(depth + 1, cur + 1);

}
int main() {
	int T;
	scanf("%d", &T);
	for (int test = 0; test < T; test++) {
		answer = 999999;
		person.clear();
		stair.clear();

		scanf("%d", &n);

		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &map[i][j]);
				if (map[i][j] == 1) 
					person.push_back(make_pair(i, j));
				if (map[i][j] >= 2)
					stair.push_back(make_pair(i, j));
			}
		}


		dfs(0,0);
		printf("#%d %d\n",test+1, answer);
	}
	return 0;
}
```

