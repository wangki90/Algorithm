```c++
#include <cstdio>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

typedef struct bottle {
	int a;
	int b;
	int c;
}bottle;

struct bottle bot;
vector<int> answer;
int chk[201][201][201];
int chk2[201];
int size_a, size_b, size_c;
void bfs() {

	queue<bottle> que;
	que.push(bot);

	chk[0][0][size_c] = 1;
	answer.push_back(size_c);
	chk2[size_c] = 1;

	while (!que.empty()) {

		int ca = que.front().a;
		int cb = que.front().b;
		int cc = que.front().c;

		que.pop();

		int na, nb, nc;
		
		if (ca > 0) {
			if (ca + cb > size_b) {
				nb = size_b;
				na = ca - (size_b - cb);
			}
			else if (ca + cb == size_b) {
				nb = size_b;
				na = 0;
			}
			else if (ca + cb < size_b) {
				nb = ca + cb;
				na = 0;
			}
			if (chk[na][nb][cc] == 0) {
				chk[na][nb][cc] = 1;
				bottle tmp;
				tmp.a = na; tmp.b = nb; tmp.c = cc;
				que.push(tmp);
				if (na == 0 && chk2[cc] == 0) {
					chk2[cc] = 1;
					answer.push_back(cc);
				}
			}

			if (ca + cc > size_c) {
				nc = size_c;
				na = ca - (size_c - cc);
			}
			else if (ca + cc == size_c) {
				nc = size_c;
				na = 0;
			}
			else if (ca + cc < size_c) {
				nc = ca + cc;
				na = 0;
			}
			if (chk[na][cb][nc] == 0) {
				chk[na][cb][nc] = 1;
				bottle tmp;
				tmp.a = na; tmp.b = cb; tmp.c = nc;
				que.push(tmp);
				if (na == 0 && chk2[nc] == 0) {
					chk2[nc] = 1;
					answer.push_back(nc);
				}
			}
		}

		if (cb > 0) {
			if (ca + cb > size_a) {
				na = size_a;
				nb = cb - (size_a - ca);
			}
			else if (ca + cb == size_a) {
				na = size_a;
				nb = 0;
			}
			else if (ca + cb < size_a) {
				na = ca + cb;
				nb = 0;
			}
			if (chk[na][nb][cc] == 0) {
				chk[na][nb][cc] = 1;
				bottle tmp;
				tmp.a = na; tmp.b = nb; tmp.c = cc;
				que.push(tmp);
				if (na == 0 && chk2[cc] == 0) {
					chk2[cc] = 1;
					answer.push_back(cc);
				}
			}

			if (cb + cc > size_c) {
				nc = size_c;
				nb = cb - (size_c - cc);
			}
			else if (cb + cc == size_c) {
				nc = size_c;
				nb = 0;
			}
			else if (cb + cc < size_c) {
				nc = cb + cc;
				nb = 0;
			}
			if (chk[ca][nb][nc] == 0) {
				chk[ca][nb][nc] = 1;
				bottle tmp;
				tmp.a = ca; tmp.b = nb; tmp.c = nc;
				que.push(tmp);
				if (ca == 0 && chk2[nc] == 0) {
					chk2[nc] = 1;
					answer.push_back(nc);
				}
			}
		}

		if (cc > 0) {
			if (ca + cc > size_a) {
				na = size_a;
				nc = cc - (size_a - ca);
			}
			else if (ca + cc == size_a) {
				na = size_a;
				nc = 0;
			}
			else if (ca + cc < size_a) {
				na = cc + ca;
				nc = 0;
			}
			if (chk[na][cb][nc] == 0) {
				chk[na][cb][nc] = 1;
				bottle tmp;
				tmp.a = na; tmp.b = cb; tmp.c = nc;
				que.push(tmp);
				if (na == 0 && chk2[nc] == 0) {
					chk2[nc] = 1;
					answer.push_back(nc);
				}
			}

			if (cb + cc > size_b) {
				nb = size_b;
				nc = cc - (size_b - cb);
			}
			else if (cb + cc == size_b) {
				nb = size_b;
				nc = 0;
			}
			else if (cb + cc < size_b) {
				nb = cb + cc;
				nc = 0;
			}
			if (chk[ca][nb][nc] == 0) {
				chk[ca][nb][nc] = 1;
				bottle tmp;
				tmp.a = ca; tmp.b = nb; tmp.c = nc;
				que.push(tmp);
				if (ca == 0 && chk2[nc] == 0) {
					chk2[nc] = 1;
					answer.push_back(nc);
				}
			}
		}

	}

}
int main() {
	
	scanf("%d %d %d", &size_a, &size_b, &size_c);
	bot.a = 0; bot.b = 0; bot.c = size_c;
	bfs();
	int x = answer.size();
	sort(answer.begin(),answer.end());
	for (int i = 0; i < answer.size(); i++) {
		printf("%d ", answer[i]);
	}
	printf("\n");

	return 0;
}
```

