```c++
//MAX HEAP(힙)
#include <cstdio>
#include <queue>

using namespace std;
int n;
priority_queue<int> pque;
vector<vector<int>> tmp;

int main() {
	int T;
	scanf("%d", &T);

	for (int test_case = 0; test_case < T; test_case++) {
		scanf("%d", &n);
		tmp.resize(T);
		for (int i = 0; i < n; i++) {
			int cmd;
			scanf("%d", &cmd);
			if (cmd == 1) {
				int x;
				scanf("%d", &x);
				pque.push(x);
			}
			else {
				if (!pque.empty()) {
					tmp[test_case].push_back(pque.top());
					pque.pop();
				}
				else {
					tmp[test_case].push_back(-1);
				}
			}
		}
	}
	for (int i = 0; i < T; i++) {
		printf("#%d", i + 1);
		for (int j = 0; j < tmp[i].size(); j++) {
			printf(" %d", tmp[i][j]);
		}
		printf("\n");
	}

	return 0;
}
```

1. 힙은 완전이진트리이기 때문에 배열로 구현하면 상당히 편리합니다.

다음과 같이 힙의 노드들에 번호를 붙여 보겠습니다. 노드 아래에 '[ ]' 안에 있는 숫자가 각 노드의 번호입니다.
트리에서의 높이가 높을수록, 높이가 같다면 왼쪽에 위치할수록 번호가 작으며 1번부터 시작합니다.

![img](https://www.swexpertacademy.com/main/common/fileDownload.do?downloadType=CKEditorImages&fileId=AV-UIY263zUDFAXr)

2. 어떤 노드의 번호가 x일 때에 다음과 같은 성질을 만족합니다.
3. x의 부모 노드 번호 = (x를 2로 나눈 몫)
4. x의 왼쪽 자식 노드 번호 = (x 곱하기 2)
5. x의 오른쪽 자식 노드 번호 = (x 곱하기 2) + 1
6. 삭제 연산을 구현할 때에, 자식 노드 2개가 모두 존재한다면 둘 중 큰 키값을 가지는 노드와 현재 노드의 위치를 바꾸어주는 식으로 구현함에 주의합니다.
7. C++의 경우, Standard Template Library로 안에 priority_queue가 있으며 최대 힙과 같은 역할을 수행합니다.



**2. priority_queue container 생성자와 연산자**

- 템플릿 선언 부분을 보겠습니다.
  **template < typename T, **
  ​                **typename Container = vector<T>,**
  ​                **typename Compare = less<typename Container::****velue_type>** **> **
  **class priority_queue;**

  ​

- 기본 생성자 형식 **priority_queue < [Data Type] > [변수이름];**
  ex) priority_queue<int> pq;

  ​

- 내부 컨테이너 변경 **priority_queue < [Data Type], [Container Type] > [변수이름];**
  ex) priority_queue<int, deque<int> > pq;

  ​

- 정렬 기준 변경 **priority_queue < [Data Type], [Container Type], [정렬기준] > [변수이름];**
  ex) priority_queue<int , vector<int>, greater<int> or less<int> > pq;

출처: 

http://blockdmask.tistory.com/107

 [개발자 지망생]