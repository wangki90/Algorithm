```c
//sprintf(char[],"%d",int) int -> char buffer
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
	int T;
	scanf("%d", &T);
	for (int tc = 1; tc <= T; tc++) {

		char c[19];
		scanf("%s", c);

		int s = 0; int c_length = 0;
		while (c[s] != '\0') {
			c_length++;
			s++;
		}

		int sum; int new_length = c_length;
		char nc[19]; strcpy(nc, c);
		while (new_length != 1) {
			sum = 0;
			for (int i = 0; i < new_length; i++) {
				int tmp = nc[i] - '0';
				sum += tmp;
			}
			sprintf(nc, "%d", sum);
			new_length = strlen(nc);
		}
		printf("#%d ", tc);
		puts(nc);
	}

	return 0;
}
```

