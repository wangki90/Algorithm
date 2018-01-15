```c++
//N-Queens
#include <cstdio>
#include <cmath>
#include <cstring>
using namespace std;
int n;
int cnt = 0;
int col[16];
bool isPos(int row) {

	for (int i = 0; i < row; i++) {
		if (col[i] == col[row] || abs(col[i] - col[row]) == abs(i - row))
			return false;
	}
	return true;
}
void solution(int depth) {

	if (depth == n - 1) {
		cnt++;
		return;
	}
	for (int i = 0; i < n; i++) {
		col[depth + 1] = i;
		if (isPos(depth + 1)) {
			solution(depth + 1);
		}
	}
}
int main() {

	scanf("%d", &n);
	memset(col, 0, sizeof(col));
	
	solution(-1);

	
	printf("%d\n", cnt);
	return 0;
}

```

