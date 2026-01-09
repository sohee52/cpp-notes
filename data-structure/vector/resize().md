# `vector::resize`의 문법과 의미

---

## 1. `resize` 기본 문법

```cpp
vector<T> v;
v.resize(new_size);
v.resize(new_size, value);
```

### 의미

* 벡터의 **크기를 `new_size`로 변경**
* 기존 원소는 유지
* 크기가 커지면 **새로 생긴 원소는 초기화됨**

---

## 2. 크기 설정 + 초기화

```cpp
tree.resize(n + 1, 0);
```

### 해석

* `tree`의 크기를 **`n + 1`로 설정**
* 새로 생긴 모든 원소를 **0으로 초기화**

즉,

```cpp
tree = vector<int>(n + 1, 0);
```

와 **동일한 효과**

---

## 3. resize 동작 규칙 정리

### (1) 크기가 커질 때

```cpp
vector<int> v = {1, 2};
v.resize(5, 0);
```

결과:

```cpp
v = {1, 2, 0, 0, 0}
```

* 새로 추가된 원소는 **두 번째 인자 값**

---

### (2) 두 번째 인자를 생략하면?

```cpp
vector<int> v = {1, 2};
v.resize(5);
```

결과:

```cpp
v = {1, 2, 0, 0, 0}   // int의 default = 0
```

> 기본 생성자가 있는 타입이면 **기본값으로 초기화**

---

### (3) 크기가 줄어들 때

```cpp
vector<int> v = {1, 2, 3, 4};
v.resize(2);
```

결과:

```cpp
v = {1, 2}
```

* 뒤의 원소는 **완전히 제거됨**
* 메모리도 해제될 수 있음

---

## 5. resize가 없으면 생기는 문제

```cpp
vector<int> tree;
update(1, 3); // ❌ tree[1] 접근 → out of bounds
```

`resize`는 **인덱스 접근을 가능하게 만드는 필수 단계**