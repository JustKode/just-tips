
# all() 함수를 이용한 복수의 키 값 체크하기
일단 `all()` 함수를 모르는 사람이 있을 것이다. `all()`은 **Python** 내장 함수로, 파라미터에 들어가는 *Iterable*의 모든 요소가 `True` 값을 가지고 있을 때, `True` 값을 반환한다. 그 이외에는 `False`를 반환 한다. 다음과 같이 구현되어있다.

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

이와 비슷한 원리로 단 하나의 값이라도 `True`를 가지고 있으면 `True`를 반환하는 `True`를 반환하는 `any()` 라는 함수가 있다. 다음과 같이 구현되어있다.

```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

## 실제 사용
자, 일단 `all()` 함수의 사용법을 알았으니 사용해 보도록 하자,  필자는 실제 `django`나 `flask`같은 서버 사이드 프레임워크를 사용할 때, **복수의 필드값 체크**시 애용하는 기법이다. 예를 들어 `request` 객체가 있다 치고, 여기에는 사용자가 보낸 정보가 다음과 같이 `dict` 객체로 이루어 졌다고 가정한다.

```python
request = {
	"id": "justkode",
	"password": "helloworld",
	"email": "sobu0715@gmail.com",
	"phone": "010-0000-0000",
	"address": "Korea"
}
```

우리는 서버에서 정당한 요청이 왔는지 체크해야 할 의무가 있다. 이런 방법을 생각할 수 있다.
```python
if "id" in request and "password" in request and "email" in request and "phone" in request and "address" in request:
	print("request success!")
```

음.. 상당히 지저분해 보인다. 하지만, 우리가 방금 배운 `all()`을 이용하면

```python
# for 문으로 iterable 객체를 생성, 요소들은 키값이 있는지 없는지가 True or False로 반환된 것.
if all(key in request for key in ("id", "password", "email", "phone", "address")):
	print("request success!")
```

훨씬 깔끔하게 **복수의 필드(키) 값**을 검사 할 수 있다.

## References
- [Python Document](https://docs.python.org/ko/3/library/functions.html)