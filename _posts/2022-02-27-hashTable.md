---
title: 알고리즘 (#1) 해시 테이블
date: 2022-02-27 21:40:00 +/-TTTT
categories: [CS,Algorithm]
tags: [algorithm, hashtable, array, list, map]
---
## 해시 테이블의 정의
해시테이블은 해시 함수를 활용해서 키 값에 인덱스를 배정하고, 인덱스의 값에 데이터를 넣는 자료 구조를 뜻함.  
<span style="color:#e74c3c">
➡️ [key:value]로 데이터를 저장하는 자료구조
</span>  
그리고 해시란, 키와 값이 한 쌍으로 구성된 데이터를 가리킴.  
![hashtable](/assets/img/hashTable/hash_table.png){: width="50%"}
<center>출처: 위키백과_해시테이블</center>

### 해시 테이블의 구성
해시테이블은 키(key), 값(value), 해시함수(hash function), 해시(hash), 배열(bucket, slot)으로 구성되어 있다.  
* What is **hash**?  
 
