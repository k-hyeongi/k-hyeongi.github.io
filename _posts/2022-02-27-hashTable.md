---
title: 알고리즘 (#1) 해시 테이블
date: 2022-02-27 21:40:00 +/-TTTT
categories: [CS,Algorithm]
tags: [algorithm, hashtable, array, list, map, chaining]
---
## 해시 테이블
해시테이블은 해시 함수를 활용해서 키를 해시값으로 매핑하고, 이 해시값을 색인(인덱스) 또는 주소 삼아 데이터를 key와 함께 저장하는 자료구조를 뜻한다.
<span style="color:#e74c3c">
➡️ [key:value]로 데이터를 저장하는 자료구조
</span>  
그리고 해시란, 키와 값이 한 쌍으로 구성된 데이터를 가리킨다.  
![hashtable](/assets/img/hashTable/hash_table.png){: width="80%"}

<center>출처: 위키백과_해시테이블</center>

### 해시 테이블의 구성
해시테이블은 키(key), 값(value), 해시함수(hash function), 해시(hash), 데이터가 저장되는 곳(bucket, slot)으로 구성되어 있다.  



처음에 해시 테이블에 대해 들었을때 총체적 난국이었다. 해시는 뭐고, 해시 함수는 뭐고, 이게 왜 효율적인 자료구조라는거야? cs는 대부분 영어를 해석해야 되기 때문에 직관적으로 이해하기는 어려운 것 같다. 그래서 하나하나 차근차근 알아가야 한다.
* What is **Hash Function**?  
해시함수는 **key를 고정된 크기의 hash로 변경해주는 함수**이다. 이 과정을 **hashing**이라고 부른다. key를 hash function에 매개변수로 넣어서 return 값으로 나오는 값이 hash라고 생각하면 된다. 그리고 **이 hash가 저장인덱스가 된다**고 생각하면 될 것 같다.

* What is **hash**?  
hash는 **색인(인덱스)**라고 편하게 생각하면 된다.
```js
function hashStringToInt(str, tableSize) {
// string 키값을 받아서 int형 인덱스로 전환해주는 함수
    let hash = 17;
    // 소수를 값으로 지정함으로서 장점은 키를 잘 분산시킬 수 있다.

    for (let i=0; i<str.length; i++) {
        hash = (7 * hash * str.charCodeAt(i)) % tableSize;
        // charCodeAt() 메서드는 주어진 인덱스에 대한 UTF-16 코드를 나타내는 0부터 65535 사이의 정수를 반환한다.
    }

    return hash;
    // hash(idx)를 리턴해주는 형태
}
```

### 해시함수
이번에 사용한 해시함수 방법은 일종의 Division Method와 각 key의 문자열을 ASCII코드로 바꿔 계산하는 방법이다.


**Division Method**: 나눗셈을 이용하는 방법으로 입력값을 테이블의 크기로 나누어 계산한다.( 주소 = 입력값 % 테이블의 크기) 테이블의 크기를 소수로 정하고 2의 제곱수와 먼 값을 사용해야 효과가 좋다고 알려져 있다.

따라서, 해시테이블은 기본적으로 key 값과 해당 key에 대응하는 value로 구성되고, 중복을 허용하지 않는 경우에 특정 key값에 대한 값을 찾는 시간 복잡도는 O(1)로 알려져 있다. 최악의 경우엔 모든 요소를 순회해야 하므로 시간 복잡도는 O(n)이 될 것이다.  

## 해시 충돌

### 해시 충돌이란?
만약에 "firstName", "lastName" 이라는 두 가지 key가 있다고 해보자. 이 때, "firstName", "lastName"을 hash function을 통해서 각각 hash를 얻었는데 이 hash가 둘다 똑같이 6이 나왔다고 해보자. 이렇게 된다면 서로 충돌이 일어나서 올바른 값을 불러오지 못하는데 이러한 현상을 **해시 충돌, Hash Collision**이라고 한다.

### 해시 충돌 해결법
해시 충돌 해결법에는 크게 2가지가 있다.
1. 연결법(Chaining)
2. 개방 주소법(Open Addressing)

여기서는 Chaining 방법을 사용해서 해시 충돌을 해결해볼 것이다.

```js
// Collapse(충돌)가 발생할 때 어떻게 대처해야 하는가
set_item = (key, value) => {
    this.numItems++;
    const loadFactor = this.numItems / this.table.length;
    if (loadFactor > .8) {
        //resize
        this.resize();
    }

    const idx = hashStringToInt(key, this.table.length);
    if (this.table[idx]) { // this.table[idx]에 이미 값이 존재할 때
        this.table[idx].push([key, value]);
        console.log(this.table[idx])
    } else {
        this.table[idx] = [[key, value]];
    }
};
```
```js
get_item = (key) => {
    const idx = hashStringToInt(key, this.table.length);

    if (!this.table[idx]) { // Simple Error Checking
        return null;
    }
    console.log(this.table[idx])
    return this.table[idx].find(x => x[0] === key)[1]; // find() 메서드는 주어진 판별 함수를 만족하는 첫 요소 값 반환. 그런 요소가 없다면 undefined 반환.
    // 
};
```
### Chaining
기존 해시테이블 구조로는, 해시 주소 하나에 하나의 슬롯이 존재해 이미 점유된 슬롯에 중복되어서는 안됐다. 하지만, chaining 기법은 점유된 슬롯을 패스하는 것이 아닌, 점유된 슬롯에 자료를 추가하는 방식으로, Linked List와 유사한 구조로 구현된다.  
해시 주소 하나에 리스트(배열)가 하나씩 배정된다면 리스트에 슬롯(일종의 노드)을 연결하는 방식으로 다른 주소로 이동하는 것을 없애는 것이다.
  
위에 내가 첨부한 코드를 보면
```js
set_item = (key, value) => {
...
if (this.table[idx]) { // this.table[idx]에 이미 값이 존재할 때
        this.table[idx].push([key, value]);
        console.log(this.table[idx])
}
...
};
```
한 해시 주소에 이미 값이 존재할 때 그 주소에 [key, value] 배열을 push함으로써 한 주소에 두 가지 슬롯이 존재하게 된다. 
```js
get_item = (key) => {
...
    if (!this.table[idx]) { // Simple Error Checking
        return null;
    }
    console.log(this.table[idx])

    return this.table[idx].find(x => x[0] === key)[1]; // find() 메서드는 주어진 판별 함수를 만족하는 첫 요소 값 반환. 그런 요소가 없다면 undefined 반환.
...
};
```
이렇게 get_item 메소드에서 리턴할 때 조건을 만족하는 요소를 find()를 통해서 반환하게 된다.

--------------------------------------------------------

## 해시 테이블 예시 공부 코드
```js
function hashStringToInt(str, tableSize) {
    let hash = 17;
    // 소수를 값으로 지정함으로서 장점은 키를 잘 분산시킬 수 있다.

    for (let i=0; i<str.length; i++) {
        hash = (7 * hash * str.charCodeAt(i)) % tableSize;

        // charCodeAt() 메서드는 주어진 인덱스에 대한 UTF-16 코드를 나타내는 0부터 65535 사이의 정수를 반환한다.
    }

    return hash;
}

class HashTable {

    table = new Array(3);
    numItems = 0;

    resize = () => {
        const newTable = new Array(this.table.length * 2);
        this.table.forEach(item => { // forEach() 메서드는 주어진 함수를 배열 요소 각각에 대해 실행합니다.
            if (item) {
                item.forEach(([key, value]) => {
                    const idx = hashStringToInt(key, newTable.length);
                    if (newTable[idx]) {
                        newTable[idx].push([key, value]);
                    } else {
                        newTable[idx] = [[key, value]];
                    }
                });
            }
        });
        this.table = newTable;
    }

    // Collapse(충돌)가 발생할 때 어떻게 대처해야 하는가
    set_item = (key, value) => {
        this.numItems++;
        const loadFactor = this.numItems / this.table.length;
        if (loadFactor > .8) {
            //resize
            this.resize();
        }

        const idx = hashStringToInt(key, this.table.length);
        if (this.table[idx]) { // this.table[idx]에 이미 값이 존재할 때
            this.table[idx].push([key, value]);
            console.log(this.table[idx])
        } else {
            this.table[idx] = [[key, value]];
        }
    };

    get_item = (key) => {
        const idx = hashStringToInt(key, this.table.length);

        if (!this.table[idx]) { // Simple Error Checking
            return null;
        }
        console.log(this.table[idx])
        return this.table[idx].find(x => x[0] === key)[1]; // find() 메서드는 주어진 판별 함수를 만족하는 첫 요소 값 반환. 그런 요소가 없다면 undefined 반환.
        // 
    };

}



const myTable = new HashTable();
myTable.set_item("firstName", "bob");
console.log(myTable.table.length);
myTable.set_item("lastName", "Tim");
myTable.set_item("age", 23);
console.log(myTable.table.length);
myTable.set_item("birthday", "2000/07/21");
console.log(myTable.table);
console.log(myTable.get_item("firstName"));
console.log(myTable.get_item("lastName"));
console.log(myTable.get_item("age"));
console.log(myTable.get_item("birthday"));

// 출처: Ben Award 유튜브 (https://youtu.be/UOxTMOCTEZk)

```
깃헙 주소  
https://github.com/k-hyeongi/Algorithm/blob/main/HashTable

출처: Ben Award 유튜브 (https://youtu.be/UOxTMOCTEZk)