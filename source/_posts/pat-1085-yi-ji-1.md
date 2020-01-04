---
title: Pat_1085（乙级）
url: 1794.html
id: 1794
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:25:36
tags:
  - pat
---

1085 PAT单位排行 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805260353126400)

每次 PAT 考试结束后，考试中心都会发布一个考生单位排行榜。本题就请你实现这个功能。

### 输入格式：

输入第一行给出一个正整数 N（≤10​5​​），即考生人数。随后 N 行，每行按下列格式给出一个考生的信息：

    准考证号 得分 学校
    

其中`准考证号`是由 6 个字符组成的字符串，其首字母表示考试的级别：`B`代表乙级，`A`代表甲级，`T`代表顶级；`得分`是 \[0, 100\] 区间内的整数；`学校`是由不超过 6 个英文字母组成的单位码（大小写无关）。注意：题目保证每个考生的准考证号是不同的。

### 输出格式：

首先在一行中输出单位个数。随后按以下格式非降序输出单位的排行榜：

    排名 学校 加权总分 考生人数
    

其中`排名`是该单位的排名（从 1 开始）；`学校`是全部按小写字母输出的单位码；`加权总分`定义为`乙级总分/1.5 + 甲级总分 + 顶级总分*1.5`的**整数部分**；`考生人数`是该属于单位的考生的总人数。 学校首先按加权总分排行。如有并列，则应对应相同的排名，并按考生人数升序输出。如果仍然并列，则按单位码的字典序输出。

### 输入样例：

    10
    A57908 85 Au
    B57908 54 LanX
    A37487 60 au
    T28374 67 CMU
    T32486 24 hypu
    A66734 92 cmu
    B76378 71 AU
    A47780 45 lanx
    A72809 100 pku
    A03274 45 hypu
    

### 输出样例：

    5
    1 cmu 192 2
    1 au 192 3
    3 pku 100 1
    4 hypu 81 2
    4 lanx 81 2

代码：
```
#include<iostream>
#include<string>
#include<algorithm>
#include<map>
#include<set>
using namespace std;
struct school {
	string id;   //再次存入id方便后来从map转入set
	map<char, int> mark;    //这里用map记录各级比赛的成绩
	int num = 0, sum = 0;   //num记录该校人数，sum为总分
};
struct cmp {         //自定义set的比较方式
	bool operator()(const school&a, const school &b) {
		if (a.sum == b.sum) {
			if (a.num == b.num)
				return a.id < b.id;
			return a.num < b.num;
		}
		return a.sum > b.sum;
	}
};
int main() {
	map<string, school> k;
	int n, t, count = 1;
	cin >> n;
	string id, name;
	while (n--) {             //录入数据
		cin >> id >> t >> name;
		transform(name.begin(), name.end(), name.begin(), ::tolower);    //将学校的字符化为小写
		k\[name\].mark\[id\[0\]\] += t;         //记住这里的+=，因为可能存在同一学校的不同学生参加了同级比赛。
		k\[name\].id = name;
		k\[name\].num++;        //该校人数计数器
	}
	set<school, cmp> rk;
	for (auto it = k.begin(); it != k.end(); it++) {    //在计算总分后将结构体插到set里面
		it->second.sum = (double)it->second.mark\['B'\] / 1.5 + it->second.mark\['A'\] + (double)it->second.mark\['T'\] * 1.5;
		rk.insert(it->second);
	}
	cout << rk.size() << endl;
	school pre;    //这里用前驱进行比较
	auto it = rk.begin();
	cout << count << " " << it->id << " " << it->sum << " " << it->num << endl;
	pre = *it;
	it++;
	int m = 2;
	for (; it != rk.end(); m++, it++) {
		if (it->sum != pre.sum)   //当前后的得分不同时，更新count
			count = m;
		printf("%d %s %d %d\\n", count, it->id.c_str(), it->sum, it->num);
		pre = *it;
	}
	return 0;
}
```