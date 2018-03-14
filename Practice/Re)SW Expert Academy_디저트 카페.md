```c++
//code refac
#include <iostream>
#include <cstdio>
#include <cstring>
#include <utility>
#include <algorithm>
using namespace std;

int n;
int a[20][20];
int chk[20][20];
int dessert[101];
int dx[] = { 1,1,-1,-1 };
int dy[] = { 1,-1,-1,1 };
int answer;
int debug[20][20];
pair<int, int> fin;
bool isFirst;
void dfs(int x, int y, int dir, int change_num, int dessert_num) {
	

	if (fin.first == x && fin.second == y && change_num == 3) {
		answer = max(answer, dessert_num - 1);
		dessert;
		return;
	}
	
	if (x < fin.first || change_num > 3)return;

	dessert[a[x][y]] = 1;

	if (!isFirst) {
		isFirst = true;
		int nx = x + dx[dir];
		int ny = y + dy[dir];
		if (nx < 0 || nx >= n || ny < 0 || ny >= n || dessert[a[nx][ny]] == 1)
			return;
		else {
			dfs(nx, ny, dir, change_num, dessert_num + 1);
		}
		return;
	}
	for (int i = 0; i <= 1; i++) {
		int nx = x + dx[(dir + i)%4];
		int ny = y + dy[(dir + i)%4];

		if (nx >= 0 && nx < n && ny >= 0 && ny < n) {		
			if(dessert[a[nx][ny]] == 0 || (nx == fin.first && ny == fin.second) )
				dfs(nx, ny, (dir + i) % 4, change_num + i, dessert_num + 1);
		}		
	}
	dessert[a[x][y]] = 0;
}
int main(int argc, char** argv)
{
	int test_case;
	int T;

	//freopen("smaple_input.txt", "r", stdin);
	scanf("%d", &T);

	for (test_case = 1; test_case <= T; ++test_case)
	{
		answer = 0;
		scanf("%d", &n);
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				scanf("%d", &a[i][j]);
			}
		}
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				memset(dessert, 0, sizeof(dessert));
				isFirst = false;
				dessert[a[i][j]] = 1;
				fin.first = i; fin.second = j;
				dfs(i, j, 0, 0, 1);
			}
		}
		if (answer == 0)answer = -1;
		printf("#%d %d\n", test_case, answer);

	}
	return 0;//정상종료시 반드시 0을 리턴해야합니다.
}
```

