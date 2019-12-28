---
title: Pat_1073（乙级）
url: 1770.html
id: 1770
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:06:57
tags:
---

1073 多选题常见计分法 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805263624683520)

批改多选题是比较麻烦的事情，有很多不同的计分方法。有一种最常见的计分方法是：如果考生选择了部分正确选项，并且没有选择任何错误选项，则得到 50% 分数；如果考生选择了任何一个错误的选项，则不能得分。本题就请你写个程序帮助老师批改多选题，并且指出哪道题的哪个选项错的人最多。

### 输入格式：

输入在第一行给出两个正整数 N（≤1000）和 M（≤100），分别是学生人数和多选题的个数。随后 M 行，每行顺次给出一道题的满分值（不超过 5 的正整数）、选项个数（不少于 2 且不超过 5 的正整数）、正确选项个数（不超过选项个数的正整数）、所有正确选项。注意每题的选项从小写英文字母 a 开始顺次排列。各项间以 1 个空格分隔。最后 N 行，每行给出一个学生的答题情况，其每题答案格式为 `(选中的选项个数 选项1 ……)`，按题目顺序给出。注意：题目保证学生的答题情况是合法的，即不存在选中的选项数超过实际选项数的情况。

### 输出格式：

按照输入的顺序给出每个学生的得分，每个分数占一行，输出小数点后 1 位。最后输出错得最多的题目选项的信息，格式为：`错误次数 题目编号（题目按照输入的顺序从1开始编号）-选项号`。如果有并列，则每行一个选项，按题目编号递增顺序输出；再并列则按选项号递增顺序输出。行首尾不得有多余空格。如果所有题目都没有人错，则在最后一行输出 `Too simple`。

### 输入样例 1：

    3 4 
    3 4 2 a c
    2 5 1 b
    5 3 2 b c
    1 5 4 a b d e
    (2 a c) (3 b d e) (2 a c) (3 a b e)
    (2 a c) (1 b) (2 a b) (4 a b d e)
    (2 b d) (1 e) (1 c) (4 a b c d)
    

### 输出样例 1：

    3.5
    6.0
    2.5
    2 2-e
    2 3-a
    2 3-b
    

### 输入样例 2：

    2 2 
    3 4 2 a c
    2 5 1 b
    (2 a c) (1 b)
    (2 a c) (1 b)
    

### 输出样例 2：

    5.0
    5.0
    Too simple

代码（本题和之前的一题十分类似）：

#include <iostream>
#include <vector>
#include <iomanip>
#include <string.h>

using namespace std;

const int LEN = 5;

struct ques {
	int score;
	int ans\[LEN\]; //答案向量，1表示含此答案，0表示不含此答案
	int ansCount;
	int wrongNum\[LEN\];//答错向量
};

int main() {

	int n, m;
	cin>>n>>m;
	ques qu\[m\];
	for(int i=0; i<m; i++) {
		memset(qu\[i\].ans, 0, sizeof(qu\[i\].ans));
		memset(qu\[i\].wrongNum, 0, sizeof(qu\[i\].wrongNum));
		qu\[i\].ansCount = 0;
	}

	double stuScore\[n\] = {0};

	for(int i=0; i<m; i++) {
		cin>>qu\[i\].score;
		int t, c;
		cin>>t>>c;
		for(int j=0; j<c; j++) {
			char ch;
			cin>>ch;
			qu\[i\].ans\[ch-'a'\] = 1;
			qu\[i\].ansCount++;
		}
	}

	string s1;
	getline(cin, s1);
	int maxWrongNum = 0;
	for(int i=0; i<n; i++) {
		getline(cin, s1);
		string s2;
		//remove blank
		for(int j=0; j<s1.length(); j++) {
			if(s1.at(j)!=' ') {
				s2 += s1.at(j);
			}
		}
		for(int j=0; j<m; j++) {
			//find one answer
			int start = s2.find("(");
			int end = s2.find(")");
			string tmp = s2.substr(start, end-start+1);
			int tmpAns\[LEN\] = {0};
			for(int k=0; k<tmp.at(1)-'0'; k++) {
				tmpAns\[tmp.at(2+k)-'a'\] = 1; //该学生选了此选项，tmp.at(2+k)是该选项，-'a'是把字母变成数字

			}
			//judge whether correct
			bool flag = true;
			int tmpCount = 0;
			for(int k=0; k<LEN; k++) {
				if(tmpAns\[k\]==1) {
					tmpCount++;
				}
				if(tmpAns\[k\]==0 && qu\[j\].ans\[k\]==1) {
					qu\[j\].wrongNum\[k\]++;
					if(qu\[j\].wrongNum\[k\]>maxWrongNum) {
						maxWrongNum = qu\[j\].wrongNum\[k\];
					}
				} else if(tmpAns\[k\]==1 && qu\[j\].ans\[k\]==0) {
					qu\[j\].wrongNum\[k\]++;
					flag = false;
					if(qu\[j\].wrongNum\[k\]>maxWrongNum) {
						maxWrongNum = qu\[j\].wrongNum\[k\];
					}
				}
			}
			//correct or semi-correct
			if(flag && tmpCount==qu\[j\].ansCount) {
				stuScore\[i\] += qu\[j\].score;
			} else if(flag) {
				stuScore\[i\] += qu\[j\].score/2.0;
			}

			s2 = s2.substr(end+1);
		}
	}

	for(int i=0; i<n; i++) {
		cout<<setiosflags(ios::fixed)<<setprecision(1)<<stuScore\[i\]<<endl;
	}
	if(maxWrongNum>0) {
		for(int j=0; j<m; j++) {
			for(int k=0; k<LEN; k++) {
				if(qu\[j\].wrongNum\[k\]==maxWrongNum) {
					cout<<maxWrongNum<<" "<<(j+1)<<"-"<<(char)(k+'a')<<endl;
				}
			}
		}
	} else {
		cout<<"Too simple"<<endl;
	}

	return 0;
}