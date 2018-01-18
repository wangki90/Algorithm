```c++
//벌꿀 채취
#include <cstdio>
#include <algorithm>
#include <vector>
#include <cmath>

using namespace std;

int n, m, c;
int map[11][11];
int max_val, p_max, tmp_max;

void dfs(int x, int y, int depth, int val, int square_val) {

   if (depth == m) {
      p_max = max(p_max, square_val);
      return;
   }

   int cur = map[x][y];
   int cur_value = val + cur;
   for (int i = depth; i < m; i++) {
      if (cur_value <= c) { //1-1.벌꿀을 더 채취 할 경우,
         dfs(x, y + 1, i + 1, cur_value, square_val + pow(cur, 2));
      }
      else {
         if (val == cur) { //1-2벌꿀을 더이상 채취 못하는데, 현재까지 채취한 벌꿀양과 현재칸의 벌꿀양			이 동일할 경우, 현재칸의 값으로 바꿔준다.
            dfs(x, y + 1, i + 1, cur, pow(cur, 2));
         }
         else { //1-3아닐 경우, 현재 칸 건너뛰고 다음칸으로.
            dfs(x, y + 1, i + 1, val, square_val);
         }
      }
     //2.벌꿀을 현재칸에서 채취하지 않은 경우,
      dfs(x, y + 1, i + 1, val, square_val);
   }
}
void selection() {

   int x1, y1, x2, y2;

   //person1, person2 시작 좌표 구하기.
   for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
         for (int q = i; q < n; q++) {
            for (int w = 0; w < n; w++) {
               for (int k = 0; k < m; k++) {
                  if (i == q)
                     x1 = i, y1 = j + k, x2 = q, y2 = y1 + m + k;
                  else
                     x1 = i, y1 = j + k, x2 = q, y2 = w + k;

                  if (y1 > n - m || y2 > n - m || x1 == x2 && y1 == y2)
                     continue;
				//각 칸마다 채취할 수 있는 최대 벌꿀양의 제곱(p_max)을 리턴받음.
                  tmp_max = p_max = 0;
                  dfs(x1, y1, 0, 0, 0);
                  tmp_max += p_max;
                  p_max = 0;
                  dfs(x2, y2, 0, 0, 0);
                  tmp_max += p_max;
                  max_val = max(max_val, tmp_max);
               }
            }
         }
      }
   }
}
int main() {

   int T;
   scanf("%d", &T);

   for (int tc = 0; tc < T; tc++) {
      max_val = p_max = 0;
      scanf("%d %d %d", &n, &m, &c);

      for (int i = 0; i < n; i++) {
         for (int j = 0; j < n; j++) {
            scanf("%d", &map[i][j]);
         }
      }

      selection();
      printf("#%d %d\n", tc + 1, max_val);
   }

   return 0;
}
```

