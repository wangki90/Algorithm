```c++
#include <cstdio>
#include <iostream>
#include <algorithm>
#include <vector>
#include <algorithm>
#include <cstring>
#include <queue>
#include <string>
#include <set>
#include <cmath>
using namespace std;
int n, k;
string str;
set<int> s;
int change_num(char c) {
	if (c == '0') {
		return 0;
	}
	else if (c == '1') {
		return 1;
	}
	else if (c == '2') {
		return 2;
	}
	else if (c == '3') {
		return 3;
	}
	else if (c == '4') {
		return 4;
	}
	else if (c == '5') {
		return 5;
	}
	else if (c == '6') {
		return 6;
	}
	else if (c == '7') {
		return 7;
	}
	else if (c == '8') {
		return 8;
	}
	else if (c == '9') {
		return 9;
	}
	else if (c == 'A') {
		return 10;
	}
	else if (c == 'B') {
		return 11;
	}
	else if (c == 'C') {
		return 12;
	}
	else if (c == 'D') {
		return 13;
	}
	else if (c == 'E') {
		return 14;
	}
	else if (c == 'F') {
		return 15;
	}
}
int convert_dex(string x, int cnt) {
	int exp = cnt - 1;
	int ret = 0;
	while (exp >= 0) {
		int num = change_num(x[cnt - (exp + 1)]);
		ret += (pow(16,exp) * num);
		exp--;
	}

	return ret;
}
bool compare(int a, int b) {
	return a > b;
}
int main() {
	int tc;
	cin >> tc;
	for (int test_case = 1; test_case <= tc; test_case++) {
		scanf("%d %d", &n, &k);
		s.clear();
		int tmp = n / 4;
		/*for (int i = 0; i < n; i++) {
			cin >> c[i];
		}*/
		cin >> str;
		string a = "", b = "", c = "", d ="";
		for (int i = 0; i < tmp; i++) {
			a += str[i];
		}
		for (int i = tmp; i < 2 * tmp; i++) {
			b += str[i];
		}
		for (int i = 2 * tmp; i < 3 * tmp; i++) {
			c += str[i];
		}
		for (int i = 3 * tmp; i < 4 * tmp; i++) {
			d += str[i];
		}

		/*cout << a << " " << b << " " << c << " " << d << endl;*/
		s.insert(convert_dex(a, tmp));
		s.insert(convert_dex(b, tmp));
		s.insert(convert_dex(c, tmp));
		s.insert(convert_dex(d, tmp));

		string new_str = str;
		for (int i = 0; i < tmp; i++) {
			char end = new_str[new_str.length() - 1];
			string tmp_str = new_str.substr(0,new_str.length() - 1);
			new_str.clear();
			new_str += end;
			new_str.append(tmp_str);

			a = "", b = "", c = "", d = "";
			for (int i = 0; i < tmp; i++) {
				a += new_str[i];
			}
			for (int i = tmp; i < 2 * tmp; i++) {
				b += new_str[i];
			}
			for (int i = 2 * tmp; i < 3 * tmp; i++) {
				c += new_str[i];
			}
			for (int i = 3 * tmp; i < 4 * tmp; i++) {
				d += new_str[i];
			}

			/*cout << a << " " << b << " " << c << " " << d << endl;*/
			s.insert(convert_dex(a, tmp));
			s.insert(convert_dex(b, tmp));
			s.insert(convert_dex(c, tmp));
			s.insert(convert_dex(d, tmp));

		}
		vector<int> saver;
		set<int>::iterator iter;
		for (iter = s.begin(); iter != s.end(); iter++) {
			/*cout << *iter << " ";*/
			saver.push_back(*iter);
		}

		sort(saver.begin(), saver.end(),compare);
		printf("#%d %d\n",test_case, saver.at(k - 1));
	}
	return 0;
}
```

