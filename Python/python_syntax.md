# Python 문법

[점프투파이썬](https://wikidocs.net/), [코드카데미](https://www.codecademy.com/) 참고. 다른 언어와 조금 달라서 기억해야할 필요가 있는 것들만 추려서 정리했다.

## 1. 주석

- 한 줄 주석: #
- 여러 줄 주석: 문자열을 만드는 방법과 동일하게 """ """ or ''' ''' 사이에 넣을 수도 있지만 PEP8에선 한 줄짜리 주석을 연속해서 쓰는 것을 권장하고 있다. 서브라임 텍스트 등 대부분의 에디터는 'cmd+/" 단축키를 지원한다.

## 2. 자료형

### A. 숫자형

|  항목  |      사용 예      |
|--------|-------------------|
| 정수   | 123, -123, 0      |
| 실수   | 1.2, -0.4, 3.4e10 |
| 복소수 | 1+2j, -3J         |
| 8진수  | 0o45, 0O42        |
| 16진수 | 0xA1, OXFF        |

- 지수 표현하기: 1의 자리 수와 소수로만 표현한다. 그리고 뒤에 e(E 동일)를 붙여서 10의 제곱수를 곱해서 표현한다. 1.23e10은 1.23에 10의 10승을 곱한 것이고, 3.45e-10은 3.45에 10의 -10승을 곱한 것이다.
- 복소수 활용: 내장함수가 있다. 복소수.real, 복소수.imag 처럼 뒤에 붙여 사용하면 순서대로 실수부와 허수부를 리턴한다. 또한 복소수.conjugate()라는 내장함수를 사용하면 켤레복소수를 리턴한다. abs(복소수)는 절대값을 리턴하는데 계산 방식은 1+2j일 때 1의 제곱과 2의 제곱을 더해서 루트씌운것이다. 

### B. 문자열

#### 1) 기본

- 문자열 나타내는 방법: '', "", ''' ''', """ """ 이렇게 4가지다.
- 문자열 합칠 때: 더하면 된다. "hihi" + "hello" => "hihihello"
- 문자열 반복시키기: 곱하면 된다. "hi"*2 => "hihi"
- 문자열 역시 iterable이다. 인덱싱과 슬라이싱 활용할 수 있다.
    + 'abc'[2] => 'c', 'abcde'[-1] => 'e', 'abc'[-0] => 'a'
    + 'abc'[:2] => 'abc', 'abcde'[1:3] => 'bcd', 'abcde'[1:-2] => 'bc'
    + 하지만 인덱싱을 활용해서 문자열의 내용을 바꿀 수는 없다. 'abc'[0] = 'A' 를 하려면 에러가 뜬다. 새로 만들어야 한다. 기존 것을 활용하고 싶다면 바꾸고 싶은 글자의 인덱스를 확인하여 전과 그 후 부분을 슬라이싱해서 이어붙이면 된다.

#### 2) 문자열 포매팅

| 코드 |           설명           |
|------|--------------------------|
| %s   | 문자열 String            |
| %c   | 문자 character           |
| %d   | 정수 Integer             |
| %f   | 부동 소수 floating-point |
| %o   | 8진수                    |
| %x   | 16진수                   |
| %%   | 퍼센트 문자 나타내기     |

- '%d %s + %' 사용 방법
    + “I eat three %ss” % “apple"
    + “I eat %d %s” % (3, “apple”)
    + “I eat %s apples” % 3 이렇게 하면 3이 문자열 형태로 치환돼서 들어감. 변수가 무슨 타입인지 모르면 그냥 %s로 다 받아도 상관없다.
    + 값을 나타내는 변수를 활용해도 된다.
    + %를 사용할 때 '%' 문자를 나타내려면 '%%' 두 번 적어야 한다. %d%%
    + %10s 우측정렬. %-10s 좌측정렬. 공백 10개
    + %.4f 4자리까지
- .format 사용 방법
    + "{0} is {1}".format(1, “hi”)
    + 역시 % 때와 마찬가지로 숫자는 문자열로 자동 변환되고 값이 아닌 변수를 활용해도 오케이.
    + 이름으로 치환 가능하고 혼용도 된다: “I ate {0} applse. so I was {sick}”.format(3, sick=“hi”)
-   .format에서 정렬하기
    + {0:<10} 좌측 정렬, {0:>10} 우측 정렬, {0:^10} 가운데 정렬 10칸 공백
    + 정렬기호(<, >, ^) 앞에 문자 하나 넣으면 그걸로 빈칸 채움. {0:_^10} 이런 식
- .format에서 소수점 표현: {0:10.4f}
- .format에서 curly bracket { }를 문자 그 자체로 표현하려면 2번 써준다. {{ }}
- 문자열 앞에 r을 붙여주면 순문자열이 된다. 즉 excape 문자 '\'를 쓰지 않아도 '\n'이나 '\t' 같은 문자를 나타낼 수 있다.

#### 3) 주요 함수들

- 문자열에서 특정 문자 개수 세기: a = ‘hobby’ a.count(‘b’)
- 문자열에서 특정 문자 위치: a.find(‘b’) 또는 a.index(‘b’)
- 문자열 삽입 join: “,”.join(‘abcd’) 를 하면 “a,b,c,d” 가 된다.
- 공백 지우기: a.lstrip(), a.rstrip() 왼쪽 오른쪽 지우기. 양쪽은 그냥 strip()
- 문자열 바꾸기 replace. 정규표현식 간편하게 만든 느낌이다.
    + a=“life is too short”
    + a.replace(“life”, “yours”)
    + a = “yours is too short” 가 됨
- split(). 나눠서 리스트에 넣음
    + () 사이에 아무것도 안넣으면 공백 기준으로 구분함
    + a=“a:b:c:d” 일 때 a.split(“:”) 하면 [‘a’, ‘b’, ‘c’, ‘d’]

### C. 리스트

#### 1) 기본

- 리스트에 다양한거 다 들어갈 수 있다. 리스트까지 들어갈 수 있음.
- 빈 리스트 생성은 a = list() or a = []
- 리스트의 리스트는 이차원배열처럼 이해하면 됨. 리스트의 리스트의 리스트는 당연하게도 삼차원배열처럼 뽑아냄
- 리스트 슬라이싱. 문자열 슬라이싱과 동일
- 리스트 더하면 합쳐진 리스트가 됨. 곱하기는 같은게 반복되서 리스트가됨.
- 리스트 수정은 그 부분 뽑아서(요소 하나만 인덱스로 뽑든, 슬라이싱으로 뽑든) 다른거 대입하면 된다. 리스트를 집어넣으면 리스트가 들어간다. 다만 한 가지 다른 것은
    + a[0] = [1, 2, 3] 으로 하면 리스트 자체가 들어가게되고
    + a[0:1] = [1, 2, 3]으로 하면 첫 칸에 요소 세 칸이 들어가는 것. 리스트가 들어가는게 아니다.
- 리스트 요소 삭제는 a[0] = [] a[1:3]=[] 식으로 빈 리스트를 대입하면 된다. 혹은 del 함수를 사용해서 del a[0] 해도 된다. del 하면 객체 자체가 지워진다. 즉 사용하던 메모리를 free 시킨다는 것을 의미한다. 즉 가비지콜렉션이며 파이썬이 자체적으로 하고 있기 때문에 메모리 사용량을 위해 굳이 따로 해줄 필요는 없다.

#### 2) 관련 함수들

- a.append('something') 요소 추가는 맨 마지막에 붙는다.
- a.sort()는 요소를 순서대로 정렬하는 것. 숫자도 되고, 문자도 된다. 오름차순.
- a.reverse()는 요소 순서를 반대로 바꾸는거. 즉 sort한 다음에 리버스하면 내림차순 정렬이 됨.
- a.index(요소) 를 하면 인덱스값을 반환.
- a.insert(index, value) 를 하면 대체가 아니라 추가가 된다. 0 인덱스에 넣으면 원래 있던 요소들이 앞으로 한 칸씩 밀린다. 즉 설정한 인덱스 이후의 요소들이 모두 한칸씩 뒤로 밀린다.
- a.remove(value)를 하면 a의 요소들 중 첫 value 요소를 제거한다. 만약 요소가 없다면 에러가 난다. 모든 요소를 다 제거하고 싶으면 try 안에 반복문 돌리는 것도 괜찮겠다.
- a.pop() 은 맨 마지막 요소 빼낸다. 매개변수로 특정 값을 넣어주면 remove와 똑같이 첫 요소를 제외한다. 다만 remove와 다른 점은 뽑은 값을 리턴한다는 것.
- a.count(1)은 1이 몇 겐지 세아려서 갯수를 리턴함
- a.extend([1,2,3])을 하면 a 리스트 뒤에 매개변수 값이 합쳐진다. a += [1, 2, 3]과 동일한 의미다. append와 다른 점은 만약 a.append([1, 2, 3]) 하면 a의 마지막에 리스트 자체가 원소로 들어간다. 리스트가 합쳐지는게 아니라 리스트가 붙는다. 즉 위의 리스트 수정에서 extend는 슬라이싱, append는 인덱싱과 매칭된다 할 수 있다.

### D. 튜플

- 리스트와 대부분 쓰는 방법이 같다. 생성은 ( )를 쓰는 것이 일반적이고 아예 안써도 된다. 예를 들어 a = 1, 2, 3 처럼.
- 수정이 불가능하다. 상수화 된 리스트라고 생각하면 될까. 이 특성이 가장 중요하다. 대부분의 메소드를 똑같이 쓸 수 있지만 수정 삭제는 안된다. 추가 메소드는 가능하다.
- 요소 한 개만 쓰려면 a = (1,) 이렇게 뒤에 콤마 붙여야 함

### E. 딕셔너리

#### 1) 기본

- a = {‘key’:’value’, ‘key’:’value’}
- 키와 밸류로 이루어짐. 키를 인덱스처럼 활용해서 밸류를 뽑아낼 수 있다.
- 키에는 숫자도 되고 문자열도 됨. 튜플도 됨. 하지만 리스트는 안됨. 키에는 변하는 값이 들어가면 안된다. 밸류에는 어떤 값이든 다 됨
- 딕셔너리에는 인덱싱이나 슬라이싱 안된다. 무조건 키를 인덱스처럼 활용해서 밸류를 뽑아내는 수밖에 없다.
- 뽑아내는거랑 같은 방식으로 썼을 때 만약 그 쌍이 없다면 추가되는 것.
- 딕셔너리에는 순서가 없음.
- 삭제는 del a[key] 형태로.
- 처음 딕셔너리를 생성할 때 {1:111, 1:222} 형태로 키를 중복시키면 랜덤으로 하나만 남는다. 뭐가 없어지고 남을지 모른다.

#### 2) 관련 함수

- a.keys() 라고 하면 딕셔너리의 키들이 뽑혀나옴. dict_keys라는 객체 형태로 뽑힘. 만약 리스트가 필요하다면 list(a.keys()) 로 형변환하면 됨. 근데 굳이 변환 안해도 반복문 쓸 수 있음.
- dict_keys 객체에선 append, insert, pop, remove, sort 메소드 사용 안된다.
- a.values() 라고 하면 dict_values 객체가 리턴됨. 키객체와 같음
- a.items()를 하면 쌍을 튜플로 각각 묶어서 dict_items 객체로 리턴함
- 다 지우려면 a.clear()
- a[key] 와 비슷하게 a.get(key) 도 됨. 다른 점은 없는걸 원했을 때 전자는 에러를 띄우지만 후자는 NONE을 출력. 후자가 나은듯. 에러 없으니
- a.get(key)를 쓸 때 만약 값이 없을 때 논 대신 다른걸 쓰려면 디폴트값 설정할 수 있다. 이렇게. a.get(key, default)
- key가 있는지 조사할 때.  key in a 쓰면 된다. 사실 in 은 리스트나 튜플, 문자열 등에서도 모두 쓰일 수 있다. True False 리턴한다.

### F. 집합(Sets)

- set은 set( list형 value ) 형태로 만든다.
    + my_set = set([1, 2, 3, 4,5,5,5,5,5]) ——> set([1, 2, 3, 4, 5])
    + my_set2 = set(‘hello’) ———> set([‘h’, ‘e’, ‘l’, ‘o’])
- 중복도 없고 순서도 없다.(index 미지원)
- list(my_set) 처럼 형변환해서 인덱스 써라.
- 교집합: & 또는 set1.intersection(set2)
- 합집합: | 또는 set1.union(set2)
- 차집합: set1 - set2 또는 set1.difference(set2)
- 집합에 추가할 때
    + 한개만 추가: set1.add(value)
    + 여러개 동시 추가: set.update([5,6,7])
- 제거. set.remove(value) 이것도 매개변수 딱 하나만 받는 함수다.

### G. 참 거짓

- 문자열, 리스트, 튜플, 사전형, 세트가 차있으면 참. 비어있으면 거짓
- a = [1, 2, 3, 4] 일 때 a 리스트를 조건으로 해서 pop으로 뽑아내면 모두 뽑힌다. 예를 들어 while(a): print(a.pop()) 대신 이렇게 하면 반복이 끝난 후 a는 빈 리스트가 된다.

### H. 변수

- a = 3, b = 3, a is b —> True 값 나옴. 같은 값을 참조하고 있는 변수이므로.
- (a, b) = 1, 2 혹은 [a, b] = [3, 4] 식으로 여러 변수에 값을 한 방에 대입할 수 있다.
- swap 하는 방법: a, b = b, a
- a = [1, 2, 3] 일 때 a를 복사한다고 b = a 하면 그냥 두 레퍼런스 변수가 같은 객체를 가리키는 것이 되어버린다. 동일한 놈을 가리키고 있음. 그래서 이러면 하나를 수정했을 때 다른 것도 자연스럽게 수정되는 것처럼 동작한다. 이러지말고 b = a[:] 처럼 활용해야 한다. 혹은 b = copy(a) 대신 얘는 from copy import copy

## 3. 제어문(if, while, for)

- value in iterable 형태 잘 쓰임. not in 도 가능.
- 'is' 와 '==' 는 같은 의미. 동시에 'is not'과 '!=' 역시 같은 의미
- 조건문에서 아무것도 하기 싫으면 pass. 아예 안적으면 오류나서 이거 적어줘야 한다.
- 가장 가까운 반복문 빠져나가는 break
- 반복문에서 아래 코드는 더 이상 실행하지 않고 다음 반복으로 넘어가는 continue
- 리스트 내포: [표현식 for 항목 in 반복가능객체 if 조건문]
- for문에서 2개씩 변수를 받을 수도 있다.
    + test_list = [[1, 2], [3, 4], (5,6)]
    + for i, j in test_list 이런 식으로 가능.
    + 근데 만약 변수를 하나로만 받으면 '[1,2] [3,4] (5,6)' 이렇게 세 뭉치로 튀어나오고, 변수를 i, j, k 세 개로 받으면 2개밖에 없는데 왜 3개 지정했냐고 에러가 난다. (루비에서는 알아서 k에 None을 넣더라. 에러 없이)
- print는 자동으로 개행한다. 없애려면 print("somethin", end=" ") 식으로 end에 원하는 문자를 지정해주면 된다. 디폴트가 개행문자인 셈이다.

## 4. 입출력

### A. 함수

- 함수의 리턴값은 오직 하나다. 두 개 이상을 리턴하는 것으로(예로 return a, b) 함수가 짜여진다면 이것은 (a,b)라는 하나의 튜플이 리턴되는 형태다. 그래서 c, d = a()  이런식으로 바로 두 개 변수에 집어넣을 수 있음.
- 매개변수로 몇 개를 받을지 모를 때 앞에 * 붙여주면 된다. 주로 *args 라고 칭하는게 컨벤션이고 원하면 args 말고 다른 단어(python)를 써도 된다. 마지막에 써줘야 함. 이 args를 쓰려면 튜플 형태로 매개변수가 들어오기 때문에 iterable 활용하는 방식으로 써주면 된다.
- 매개변수가 입력되지 않았을 때 디폴트값(초기값)을 설정할 수 있다. 변수 뒤에 = 값 하면 된다. 대신 맨 뒤에 넣어야 함.
- 함수 내의 변수 효력 범위
    + a = 1 이라고 변수 a를 설정해놨을 때, 이 a 변수를 매개변수로 받아서
    + def vartest(n): n+=1 이라는 함수를 실행했다고 하자.
    + vartest(a) 라고 실행해도 a값은 변하지 않는다.
    + 정말 단순히 함수 내의 지역변수일 뿐이다. 값만 전달받은 것 뿐(call by value), 그 값 자체를 변화시키지(call by reference) 않는다.
    + 1을 증가시킨 값을 리턴해서 원래 변수에 다시 대입하는 방식밖에 없다.

### B. 입력과 출력

- print에서 print('hi' 'hi' 'hi')처럼 붙여쓰면 +랑 똑같고, 콤마(,)로 이으면 띄워써진다. print(‘hi’, ‘hi’, ‘hi’)
- 사용자 입력은 input() 해주면 된다. 리턴값은 입력받은 값이고, 매개변수로 문자열을 넣으면 콘솔에 "입력하세요: " 이런 문구로 사용된다.

### C. 파일 읽고 쓰기

#### 1) 파일 스트림 열고 닫기

- 아래 코드가 가장 일반적인 포맷이다. 즉 '파일객체 = open(파일이름, 모드)' 형태.
- 모드는 r, w, a가 있고 순서대로 읽고, 쓰고, 추가한다.

```python
# 디렉토리에서 ~ 단축키는 안 먹힌다. 절대경로 쓰려면 다 적어줘야 함
f = open("/Users/gyubin/Desktop/hi.txt", 'w')
f.close()
```

#### 2) 읽기 함수

- f.read() : 파일의 모든 데이터를 읽어온다. 모든 데이터를 읽어왔다면 다시 이 함수를 실행했을 때 빈 문자열 ""을 리턴한다.
- f.read(Integer) : 숫자크기 만큼만 글자를 읽어온다. 3을 넣으면 3글자씩 읽어온다. 실행할 때마다 정한 크기만큼 글자를 읽어오고 모두 읽어왔을 때는 역시 빈 문자열 ""를 리턴한다.
- f.readline() : '\n'이 발견될 때까지 개행문자를 포함해서 읽어온다. 즉 한 줄씩 읽어온다. 파일이 개행문자 없이 끝난다면 파일 끝까지 읽어들인다. 역시 파일 끝에 도달한 후에는 빈 문자열 ""이 리턴된다.
    + 재밌는 현상 1: 만약 write 함수를 이용해서 f.write('hi\n') f.write('hello\n') 이 두 명령어를 실행했다고 하자. 그리고 파일을 에디터로 열어보면 hi와 hello 딱 두 줄만 있다.
    + 재밌는 현상 2: 현상 1에 f.write('\n')이 추가로 실행한다면 세 번째 줄에 공백라인이 하나 더 있다.
    + 재밌는 현상 3: 에디터에서 바로 위의 예처럼 hi와 hello 딱 두 줄만 적고 저장해서 f.readline() 해보면 hello 뒤에는 '\n' 문자가 없이 나온다.
    + 재밌는 현상 4: 그런데 만약 현상 3에 추가로 한 줄을 띄워서 공백 라인을 하나 만든다면 'hi\n', 'hello\n'이 됨은 물론 '\n'이라는 놈이 하나 또 나온다.
    + '\n'의 의미: '보여지는' 관점에서 개행문자의 의미는 에디터에서 개행문자를 기준으로 이전 문자열과 이후 문자열은 줄을 나눠서 보여라!는 의미다. 반대로 '입력하는' 관점에서 개행문자의 의미는 그 다음 줄부터 입력할 준비가 되었다!는 의미다.
    + 에디터에서 엔터키: 단순히 엔터키를 치기 전까지의 편집하던 줄 끝에 개행문자를 붙이는게 아니다. 엔터키를 친 이후 넘어간 라인의 끝에도 자동으로 개행문자를 붙인다. 즉 에디터에서 엔터키란 이전 라인, 이후라인 모두의 끝에 개행문자를 붙인다는 의미다.
    + 결론: 의미없다. 그냥 뭐가 다른지 궁금했을 뿐이다. 하나 정하자면 f.write을 통해 데이터를 입력할 때 에디터에서 마지막에 한 줄 공백라인을 보이고싶다면 파일 끝에 개행문자를 2개 넣어라. f.write('end of file\n\n'
- for line in f: print(line, end="")
    + f 파일 객체에서 바로 반복문을 돌릴 수 있다. readline()처럼 개행문자까지 읽어들인다. 즉 한 줄씩 line 변수에 문자열로 할당된다.
    + readline()과 달리 콘솔에 출력하면 개행문자가 보이지 않는다. 보여지는 대신 에디터에서처럼 개행이 적용되어 출력된다. 그래서 개행문자가 연달아 입력되어있다면 공백 라인이 여러줄 출력되기도 한다.
    + print 함수가 기본적으로 개행을 하기 때문에 end=""를 적어줘서 중복되지 않게 해야 한다.
    + 가장 빠르고 효율적인 코드라고 공식문서에 적혀있다. 

#### 3) 쓰기 함수

- f.write(str_data): str_data에 들어있는 값을 파일에다가 쓴다. str_data는 문자열이어야 한다. 숫자거나 boolean이라면 에러난다. 리턴값은 쓰여진 문자열의 문자 개수다. "hi\n"을 입력했다면 3이 리턴된다.
- JSON 파일로 저장하기!: 파이썬 데이터를 JSON으로 바꾸는 것을 serializing, JSON to Python Data를 deserializing이라고 한다.
    + import json
    + json.dumps(object) : 괄호 안에 넣은 object를 serializing한 문자열을 리턴한다. 1은 '1', 'abc'는 "'abc'", [1, 2, 'abc']는 "[1, 2, 'abc']"로 바꿔준 값을 리턴하는 것. 결국 이 문자열을 파일 스트림을 쓰기모드로 my_json.json 이란 이름으로 열어서 쓰면 json 파일이 만들어지는 것이다.
    + json.dump(object, FILE) : s가 없어진 그냥 dump다. 매개변수로 저장할 객체와 쓰기 모드로 열린 파일 스트림 객체를 받는다. 이 코드를 실행하면 객체를 serializing한 문자열을 파일 스트림과 연결된 json 파일에 쓴다. 리턴값은 따로 없다. => [1, 2, 3]을 '[1, 2, 3]' 문자열로 바꿔서 파일에 쓰고, 파일을 에디터에서 열어보면 [1, 2, 3] 이라고 적혀있다.
    + var = json.load(FILE) : load 함수는 json 파일과 읽기 모드로 연결된 파일 객체를 매개변수로 받는다. 그리고 json 파일을 deserializing해서 데이터 객체로 만든 후 var 변수에 할당한다.
- 즉 정리하면 "쓰기모드 파일객체 + json.dump"와 "읽기모드 파일객체 + json.load" 요렇게만 잘 쓰면 끝이다.

#### 4) 기타 관련 함수

- with: 함수가 시작되면 파일이 열리고, 함수가 끝나면 파일이 닫힌다.
```python
with open("foo.txt", "w") as f:
    f.write("Life is too short, you need python")
```
- sys: 파일을 python으로 실행할 때 파일 외부에서 매개변수로 데이터를 받아올 수 있게 한다. 예를 들어 아래 코드가 sys1.py 라는 파일이라면 'python sys1.py' 로 코드를 실행할 것이다. 여기서 python 명령어 다음에 오는 것이 매개변수다. sys.argv는 이 매개변수들을 여러개 받아서 저장한 '리스트'다. 'python sys1.py aaa bbb ccc' 라고 명령어를 터미널에서 실행하면 aaa bbb ccc가 출력될 것이다. 아래 코드에선 2번째 원소부터 반복을 돌렸는데 첫 원소부터 돌리면 첫 번째 원소는 "sys1.py" 일 것이다.
```python
# 파일명: sys1.py, 명령어: python sys1.py aaa bbb ccc
import sys
args = sys.argv[1:] 
for i in args: 
    print(i)
# => aaa
#    bbb
#    ccc
```

## 5. 고급(? 초보자에겐)

### A. 날짜 사용

- ```from datetime import datetime ``` : datetime module에서 datetime 클래스를 가져온다.
- ```now = datetime.now()``` : 현재 시간(연월일시분초)을 객체로 담아 리턴한다.
- now 객체에서 year, month, day, hour, minute, second를 ```now.year``` 형태로 호출할 수 있다. 문자열 형태로 리턴된다.
- 공식 문서 [datetime](https://docs.python.org/3.5/library/datetime.html)

### B. 클래스

기본 구조는 다음과 같다.

```python
class MyClass(ParentClass):
    <클래스 변수 1>
    <클래스 변수 2>
    ...
    def 클래스함수1(self[, 인수1, 인수2,,,]):
        <수행할 문장 1>
        <수행할 문장 2>
        ...
    def 클래스함수2(self[, 인수1, 인수2,,,]):
        <수행할 문장1>
        <수행할 문장2>
        ...
    ...
```

- 클래스 내 함수에서 인스턴스 변수를 쓰려면 매개변수로 self를 넣어줘야 한다.
- ```def __init__(self, *args): ~~``` : init 함수는 생성자라고도 하며 인스턴스가 만들어질 때 항상 실행된다.
- 클래스 상속은 뒤에 ( ) 안에 상속받을 클래스를 적어주면 된다.
- 연산자 오버로딩: 객체끼리 +, -, *, / 등의 연산을 할 수 있다. 예를 들어 A라는 클래스에 ```__add__``` 함수를 추가하면 + 연산이 가능하다. A로 만든 a 객체가 앞에 있든 뒤에 있든 + 연산은 수행 가능하지만, self의 적용은 달라진다. a + b 인 경우 self는 a이고, b + a 인 경우에 self는 b이다. 두 객체 중 하나에만 add가 있으면 된다.

## 6. 몇 가지 함수들

- ```isalpha()``` : 문자열이 오로지 알파벳으로만 이루어져있는지
- ```isdigit()``` : 문자열이 오로지 숫자로만 이루어져있는지

## 기타

- [로또 실습 예제](http://luckyyowu.tistory.com/209)
- 주식 관련 API 자료: [모네타 블로그](http://blog.moneta.co.kr/mippy644/5990290/3983039), [archnixx 블로그](http://archnixx.tistory.com/entry/각-증권사별-API-현황)