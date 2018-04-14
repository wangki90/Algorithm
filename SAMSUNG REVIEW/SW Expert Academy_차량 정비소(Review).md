```c++
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <queue>

using namespace std;
typedef struct customer {
	int idx;
	int c_time;
	int AA;
	int BB;
}customer;
int n, m, k, a, b;
int a_t[9], b_t[9];
queue<customer> queA, queB, queC;
customer cstm[1000];
int solution() {

	int time = 0;
	int recept_desk[9], repair_desk[9];
	int recept_cnt = 0, repair_cnt = 0;
	for (int i = 0; i < 9; i++) {
		recept_desk[i] = -1;
		repair_desk[i] = -1;
	}

	//queA에 모든 고객 넣는다

	for (int i = 0; i < k; i++) {
		queA.push(cstm[i]);
	}

	while (1) {

		for (int i = 0; i < n; i++) {
			if (cstm[recept_desk[i]].c_time <= time && recept_desk[i] != -1) {
				queB.push(cstm[recept_desk[i]]);
				recept_desk[i] = -1;
				recept_cnt--;
			}
		}
		while (!queA.empty()) {

			//도착시간보다 크고, recept_desk에 비어있는 창구가 있으면,
			if (queA.front().c_time <= time && recept_cnt < n) {
				for (int i = 0; i < n; i++) {
					if (recept_desk[i] == -1) {
						cstm[queA.front().idx].AA = i + 1;
						recept_desk[i] = queA.front().idx;
						cstm[queA.front().idx].c_time = time + a_t[i];
						queA.pop();
						recept_cnt++;
						break;
					}
				}
			}
			else {
				break;
			}
		}

		for (int i = 0; i < m; i++) {
			if (cstm[repair_desk[i]].c_time <= time && repair_desk[i] != -1) {
				queC.push(cstm[repair_desk[i]]);
				repair_desk[i] = -1;
				repair_cnt--;
			}
		}

		while (!queB.empty()) {

			if (queB.front().c_time <= time && repair_cnt < m) {
				for (int i = 0; i < m; i++) {
					if (repair_desk[i] == -1) {
						cstm[queB.front().idx].BB = i + 1;
						repair_desk[i] = queB.front().idx;
						cstm[queB.front().idx].c_time = time + b_t[i];
						queB.pop();
						repair_cnt++;
						break;
					}
				}
			}
			else {
				break;
			}
		}


		if (queC.size() == k) 
			break;	

		time++;
	}

	int total = 0;
	bool flag = false;
	while (!queC.empty()) {
		if (queC.front().AA == a && queC.front().BB == b) {
			total += queC.front().idx + 1;
			flag = true;
		}
		queC.pop();
	}

	if (!flag)
		return -1;

	return total;
}
void init() {
	while (!queA.empty()) {
		queA.pop();
	}
	while (!queB.empty()) {
		queB.pop();
	}
	while (!queC.empty()) {
		queC.pop();
	}
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("input.txt", "r", stdin);
	cin >> T;

	for (test_case = 1; test_case <= T; ++test_case)
	{
		
		scanf("%d %d %d %d %d", &n, &m, &k, &a, &b);
		//init();

		for (int i = 0; i < n; i++) {
			scanf("%d", &a_t[i]);
		}
		for (int i = 0; i < m; i++) {
			scanf("%d", &b_t[i]);
		}

		for (int i = 0; i < k; i++) {
			cstm[i].idx = i;
			scanf("%d", &cstm[i].c_time);
		}

		printf("#%d %d\n", test_case, solution());

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

