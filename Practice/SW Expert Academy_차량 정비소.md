```c++
#include <cstdio>
#include <algorithm>
#include <vector>
#include <queue>

using namespace std;
int n, m, k, a, b;
vector<int> reserveTime; //각 접수창구마다 걸리는 시간 저장
vector<int> fixTime; //각 정비창구마다 걸리는 시간 저장
queue<int> visitTime; //고객이 온 시간 저장
vector<int> va; //특정 접수 창구 이용 고객 저장
vector<int> vb; // 특정 정비 창구 이용 고객 저장
queue<pair<int,int> > wq1; //웨이팅큐1
queue<pair<int,int> > wq2; //웨이팅큐2
vector<pair<int, int> > reserve; //접수창구 이용 고객 저장, <인덱스, 접수창구 완료 시간>
vector<pair<int, int> > fix; //정비창구 이용 고객 저장, <인덱스, 정비창구 완료 시간>
void solution() {
	int time = 0; //시간
	int idx = 1;
	int tmp = 0; //일을 모두 마친 인원 수
	
	while (1) {
		
		//wq1로 이동
		while (!visitTime.empty()) { //고객 도착 시간이면 웨이팅큐1에 푸쉬
			if (time == visitTime.front()) {
				wq1.push(make_pair(idx++, visitTime.front()));
				visitTime.pop();
			}
			else
				break;
		}

		//wq2,접수 창구로 이동
		for (int i = 0; i < n; i++) {
			//접수창구 -> 웨이팅큐2로 이동
			if (time >= reserve[i].second &&reserve[i].second != -1) {
				wq2.push(make_pair(reserve[i].first, reserve[i].second));
				reserve[i] = make_pair(-1, -1);
			}
			//웨이팅큐1 -> 접수창구
			if (reserve[i].first == -1 && !wq1.empty()) {
				reserve[i] = wq1.front();
				reserve[i].second = time + reserveTime[i];
				wq1.pop();
				if (i == a - 1) { //a번 창구 이용한 고객 저장
					va.push_back(reserve[i].first);
				}
			}
		}

		//정비 창구로 이동
		for (int i = 0; i < m; i++) {
			//정비창구 -> 끝
			if (fix[i].second <= time && fix[i].second != -1) {
				fix[i] = make_pair(-1, -1);
				tmp++;
			}
			//웨이팅큐2 -> 정비창구
			if (fix[i].first == -1 && !wq2.empty()) {
				fix[i] = wq2.front();
				fix[i].second = time + fixTime[i];
				wq2.pop();
				if (i == b - 1) { //b번 창구 이용한 고객 저장
					vb.push_back(fix[i].first);
				}
			}
		}

		if (tmp == k) //일을 마친 인원이 총 인원수와 같으면 종료.
			break;
		
		time++;
	}
}
void init() {
	reserve.clear();
	reserve.resize(n);
	reserve.assign(n, make_pair(-1, -1));
	fix.clear();
	fix.resize(m);
	fix.assign(m, make_pair(-1, -1));
	va.clear();
	vb.clear();
	reserveTime.clear();
	fixTime.clear();
}
int main() {
	int T;
	scanf("%d", &T);
	for (int test = 0; test < T; test++) {
		
		scanf("%d %d %d %d %d", &n, &m, &k, &a, &b);
		
		init();

		for (int i = 0; i < n; i++) {
			int x;
			scanf("%d", &x);
			reserveTime.push_back(x);
		}
		for (int i = 0; i < m; i++) {
			int x;
			scanf("%d", &x);
			fixTime.push_back(x);
		}
		for (int i = 0; i < k; i++) {
			int x;
			scanf("%d", &x);
			visitTime.push(x);
		}
		solution();
		int sum = 0;
		for (int i = 0; i < va.size(); i++) {
			for (int j = 0; j < vb.size(); j++) {
				if (va[i] == vb[j])
					sum += va[i];
			}
		}
		if (sum == 0)sum = -1;
		printf("#%d %d\n",test+1, sum);
	}

	return 0;
}
```

