```c++
//같은 충전량의 AP가 존재할 수 있음
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <vector>
#include <algorithm>
#include <cstring>
#include <queue>
#include <functional>
using namespace std;
typedef struct ap {
	int x;
	int y;
	int c;
	int p;
	int idx;
}ap;
int map[11][11];
pair<int, int> personA, personB;
vector<int> moveA, moveB;
vector<ap> charger;
int m, a;
int answer;
int dx[] = { 0,0,1,0,-1 };
int dy[] = { 0,-1,0,1,0 };
int q = 0;
int pre = 0;
bool compare(ap a, ap b) {
	return a.p > b.p;
}
void solution() {

	vector<ap> alist, blist;
	//가능한 ap 저장
	for (int i = 0; i < charger.size(); i++) {
		if (abs(charger[i].x - personA.first) + abs(charger[i].y - personA.second) <= charger[i].c) {
			alist.push_back(charger[i]);
		}
		if (abs(charger[i].x - personB.first) + abs(charger[i].y - personB.second) <= charger[i].c) {
			blist.push_back(charger[i]);
		}
	}
	//큰 순서대로 sort
	sort(alist.begin(), alist.end(), compare);
	sort(blist.begin(), blist.end(), compare);
	// 둘다 ap 개수가 1개 + ap가 같을경우만 분배, p가 같은게 있을 수 있음
	if (alist.size() > 1 && blist.size() > 1) {
		if (alist[0].p != blist[0].p) {
			answer += (alist[0].p + blist[0].p);
		}
		else {
			if (alist[0].idx != blist[0].idx) {
				answer += (alist[0].p + blist[0].p);
			}
			else {
				if (alist[1].p > blist[1].p) {
					answer += (blist[0].p + alist[1].p);
				}
				else {
					answer += (alist[0].p + blist[1].p);
				}
			}
		}
	}

	else if (alist.size() == 1 && blist.size() > 1) {
		answer += alist[0].p;
		if (alist[0].p != blist[0].p || alist[0].idx != blist[0].idx) {
			answer += blist[0].p;
		}
		else {
			answer += blist[1].p;
		}
	}
	else if (alist.size() > 1 && blist.size() == 1) {
		answer += blist[0].p;
		if (alist[0].p != blist[0].p || alist[0].idx != blist[0].idx) {
			answer += alist[0].p;
		}
		else {
			answer += alist[1].p;
		}
	}

	else if (alist.size() == 1 && blist.size() == 1) {
		if (alist[0].p == blist[0].p && alist[0].idx == blist[0].idx)
			answer += alist[0].p;
		else
			answer += (alist[0].p + blist[0].p);
	}

	else if (alist.size() == 0 && blist.size() > 0) {
		answer += blist[0].p;
	}

	else if (blist.size() == 0 && alist.size() > 0) {
		answer += alist[0].p;
	}

}
void init() {
	moveA.clear();
	moveB.clear();
	charger.clear();
	moveA.push_back(0);
	moveB.push_back(0);
	answer = 0;
}
int main() {

	int T;
	cin >> T;
	for (int test_case = 1; test_case <= T; test_case++) {

		init();
		scanf("%d %d", &m, &a);
		for (int i = 0; i < 2; i++) {
			for (int j = 0; j < m; j++) {
				int x;
				scanf("%d", &x);
				if (i == 0)
					moveA.push_back(x);
				else
					moveB.push_back(x);
			}
		}
		for (int i = 0; i < a; i++) {
			ap tmp;
			scanf("%d %d %d %d", &tmp.y, &tmp.x, &tmp.c, &tmp.p);
			tmp.x--; tmp.y--;
			tmp.idx = i;
			charger.push_back(tmp);
		}

		personA = make_pair(0, 0);
		personB = make_pair(9, 9);

		for (int i = 0; i < moveA.size(); i++) {
			personA.first += dy[moveA[i]]; personA.second += dx[moveA[i]];
			personB.first += dy[moveB[i]]; personB.second += dx[moveB[i]];
			solution();
		}
		
		
		
		printf("#%d %d\n", test_case, answer);
	}



	return 0;
}
```

