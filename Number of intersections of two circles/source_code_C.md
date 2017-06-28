```c

```

#include <stdio.h>
#include <math.h>
#include <stdlib.h>
int FindNum(int, int, int, int, int, int);
int main() {

	int x1, y1, r1, x2, y2, r2, T, *Answer;
	scanf("%d", &T);
	
	Answer = (int*)malloc(sizeof(int)*T);
	for (int i = 0; i < T; i++) {
		
		scanf("%d %d %d %d %d %d", &x1, &y1, &r1, &x2, &y2, &r2);
		Answer[i] = FindNum(x1,y1,r1,x2,y2,r2);
	}
	
	for (int i = 0; i < T; i++) printf("%d\n", Answer[i]);
	
	free(Answer);
	return 0;
}

int FindNum(int x1, int y1, int r1, int x2, int y2, int r2) {

	double d = sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2)); // 두 정점 사이의 거리, double로 선언 주의!
	int rl, rs;
	
	if (r1 > r2) {
		rl = r1;
		rs = r2;
	}
	else {
		rl = r2;
		rs = r1;
	}
	
	if (d == 0) {
		if (rl == rs) return -1; //infinite
		else return 0;
	}
	else if (rl + rs == d || rl - rs == d) return 1; //one point
	else if (rl - rs < d && rl + rs > d) return 2; //two point
	else return 0; // no point
	
	return 0;
}