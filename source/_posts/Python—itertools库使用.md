---
title: Python—itertools库使用

categories:
  - Python

tags:
  - itertools
  - Python
---

# Python—itertools库使用
## itertools.product()
重复使用words 3次进行元素间的组合，总共是3×3×3=27中情况。  

```
words = ["word", "good", "best"]
print(list(itertools.product(words, repeat=3)))

结果：
[('word', 'word', 'word'), ('word', 'word', 'good'), ('word', 'word', 'best'), ('word', 'good', 'word'), ('word', 'good', 'good'),
('word', 'good', 'best'), ('word', 'best', 'word'), ('word', 'best', 'good'), ('word', 'best', 'best'), ('good', 'word', 'word'),
('good', 'word', 'good'), ('good', 'word', 'best'), ('good', 'good', 'word'), ('good', 'good', 'good'), ('good', 'good', 'best'),
('good', 'best', 'word'), ('good', 'best', 'good'), ('good', 'best', 'best'), ('best', 'word', 'word'), ('best', 'word', 'good'),
('best', 'word', 'best'), ('best', 'good', 'word'), ('best', 'good', 'good'), ('best', 'good', 'best'), ('best', 'best', 'word'),
('best', 'best', 'good'), ('best', 'best', 'best')]
```

## itertools.combinations()
内部有序自己组合，要求长度小于列表自身长度。  

```
words = ["word", "good", "best"]
print(list(itertools.combinations(words, 3)))

结果：
[('word', 'good', 'best')]

words = ["word", "good", "best"]
print(list(itertools.combinations(words, 2)))

结果：
[('word', 'good'), ('word', 'best'), ('good', 'best')]
```

## itertools.permutations()
内部无序自组合

```
words = ["word", "good", "best"]
print(list(itertools.permutations(words, 3))) # 3为列表长度

结果：
[('word', 'good', 'best'), ('word', 'best', 'good'), ('good', 'word', 'best'), ('good', 'best', 'word'), ('best', 'word', 'good'), ('best', 'good', 'word')]
```