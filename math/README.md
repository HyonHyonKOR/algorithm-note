# 알고리즘 노트(파이썬)

### 이진수 
> 십진수를 2로 나누어 나머지(0,1)을 뒤집는다. <br>
> 즉 처음 나눈 후의 나머지는 2진수 기준, 가장 끝 자리이다. <br>

> ex) 13/2 = 6...1 <br>
       6/2 = 3...0 <br>
       3/2 = 1...1 <br>
       1<br>

  결과 13 -> 1101 <br>     

```py
before_bin = int(input())

after_bin =''
while before_bin > 0:
    if before_bin % 2 ==0:
        after_bin += '0'
    else:
        after_bin += '1'

    before_bin //= 2  

after_bin = after_bin[::-1] 
print(after_bin)
```

> 물론 파이썬의 bin() 함수로 처리하면 0b(2진수) 결과가 반환되지만, 원리 공부를 위해 알고리즘으로 푼다<br>

### 피보나치 수열
> an = an-1 + an-2 <br>
> 1,1,2,3,5,8...のように、（n-2)番目の項と(n-1)番目の項の合がn番目の項になる数列。

```py
def fib(n):
  a,b= 1,1
  if n==1 or n==2:
      return 1
  for i in range(1,n):
     a,b = b,a+b
     return a
```


### 약수 1 (기초 알고리즘)
> 하나의 자연수를 나누어 떨어지게 하는 수이다.<br>
> 나누어 떨어진다는 뜻은 몫만 존재하며 나머지가 없다는 의미이다.

> 예를 들어 10이라는 자연수를 2로 나눈다고 생각해보자. <br>

> ex) 10 / 2 = 5 ... 0 <br>
> 10을 2로 나누면 몫은 5, 나머지는 0이다.<br>
> 나머지가 0이란 뜻은 나머지가 없다는 뜻과 동일하므로 2는 10의 약수이다.
  
> 이를 코드로 표현하면 10%2 == 0로 표현할 수 있다. <br>
> 즉 N % i == 0이면 i는 N의 약수이다. 

```python

n = int(input())
arr = []

for i in range (1,n+1) :
  if n % i == 0: 
      arr.append(i) 

print(arr) # 약수 리스트
print(len(arr)) # 약수의 갯수 
```


### 약수 2
> a * b = N이면 a와 b는 N(자연수)의 약수이다. <br>

> 10 / 2 = 5 ...0 이므로 몫은 5, 나머지는 0, 약수는 2인 것을 증명했다. <br>
> 여기에서 약수인 2와 몫인 5를 곱하면? <br>
> 2 * 5 == 10이 나오는 현상을 발견할 수 있다. <br>
> 여기에서 알 수 있는 것은 두 가지이다. <br>

>1. 약수(2)와 몫(5)를 곱하면 소속된 자연수(10)가 된다. <br> 
>2. 「a * b = N이면 a,b는 약수」이다 공식이 적용되므로 2와 5 둘 다 약수인 것을 알 수 있다.<br> 

> 즉 10/2 = 5 ...0 에서 2는 물론, 몫인 5도 10의 약수가 된다.
ex> N % i == 0 이면 i뿐만 아니라 N//i도 약수이다.

```py
n = int(input())
arr = []

for i in range(1,n+1):
  if n % i == 0:
    arr.append(i)
    arr.append(n//i)
```

>하지만 위의 코드는 중복된 수가 존재한다. <br>
>1,10  2,5  5,2  10,2 로 약수가 두 번씩 들어가기 때문이다.


### 약수 3 (성능 개선 알고리즘)
>a * b  = N이면 두 약수 a,b는 대칭한다. <br>
>a * a  = N이면 a는 약수이자 제곱근이다. 즉 제곱근도 약수이다.<br>

>10의 약수는 [1,2,5,10] 이며 1 x 10, 2 x 5는 10인 것을 알 수 있다. <br>
>주목할 부분은 바로 거리이다.<br>

>100의 약수로 다시 한 번 관찰해보자<br>
>[1 2 4 5 10 20 25 50 100]  <br>
>이 경우도 가장 가까운 1과 가장 먼 100이 대칭하며 그 옆에 존재하는 2,50도 대칭하는 것을 알 수 있다.<br>

>또한 중요한 포인트로 가운데에 있는 10은 대칭하는 수가 존재하지 않는다.<br>
>하지만 10을 제곱하면 100이 된다.<br>
>이렇게 같은 수를 제곱해서 N이 되면 그 같은 수가 N의 제곱근이며 약수에도 포함되는 것을 알 수 있다.<br>

> 그러므로, 어떠한 자연수 N의 약수를 구하고 싶은 경우,<br>
> 우선 자연수 N의 제곱근까지만 반복한다.
> 약수 2 에서 증명한 것처럼 나머지 약수(20,25,50,100)는 몫을 통해 추가하면 된다.

> n -> int(n**(1/2)) <br>
> n 곱하기 1/2는 제곱근은 의미한다. n ** (1/2) 는 n의 2분의 1 제곱이라는 뜻이다. <br> 

> 100의 제곱근은 10이므로 정수이지만 10의 제곱근은 3.xxxx이므로 int()를 사용하여 정수로 변환한다.<br>
> 1번, 2번 반복은 해도 2.8번, 3.xxx번 반복한다는 건 이상하죠? 그러니까 정수로 변환이 필수이다. <br>


```py
n = int(input())
arr = []

for i in range(1,int(n**(1/2))+1):
  if n % i == 0:      # n의 제곱근까지의 약수는 반드시 추가된다. n이 100이면 range는 (1,11)이 되기 때문이다.
    arr.append(i)
    if i * i != n:    # i의 제곱이 n이 아니면, i는 n의 제곱근이 아니므로 약수 i로 나눈 몫(대칭하는 약수)를 추가한다. 
      arr.append(n//i)  # 이 if문을 추가하지 않으면 제곱근이 정수인 경우(100과 10), 10이 두 번 추가 되므로 10이 list에 두 번 추가 되어 버린다.
```

### 최대공약수 (유클리드 호제법),  최소 공배수

> 최소 공배수는 두 수의 곱을 최대 공약수로 나눈 수이다.

```py
# a = 100 b =28 우선 a가 b보다 크다고 가정

a = 100
b = 50 

def gcd(a,b):
    while b != 0:
       a,b = b,a %b
     return a

def lcm(a,b)
    return a * b / gcd(a,b)

```


### 소수 1 (하나의 숫자가 소수인지 판별)
> 1과 자기 자신만을 약수로 갖는 수를 소수라고 한다. <br>
> 즉 2개의 약수만을 가지고 있다.<br>

>ex) 7은 1과 7과 뿐만이 약수이므로 소수이다.

> 즉 반복문은 돌릴 경우, 반례를 들어 찾는 것이 정석이다. <br>
> 어떤 수 N의 소수라면 1과 N만이 약수이다. <br>
> **즉 2부터 N-1까지 단 한 번이라도 약수가 존재한다면 그 수는 소수가 아니라는 의미이다.** <br>

> 1,7을 제외한 2~6부터 싸그리 반복문을 돌려서 N%i==0이면 i는 약수가 되므로, N은 소수가 될 수 없다. <br>

```python
def is_prime_number(n):
    if n < 2:  
        return False
    for i in range(2, int(n**(1/2)) + 1):    #약수 3 알고리즘으로도 모든 약수를 찾을 수 있으므로 
        if n % i == 0:
            return False
    return True    # 반복문에서 False를 리턴하지 않고 끝까지 돌면 실행되는 코드
```


###  소수 2 (하나의 숫자가 소수인지 판별)
> N이 소수가 아니라면,  N보다 작은 소수나 √n보다 작은 소수가 존재한다(아마 소인수 관련 공부해야 할듯)<br>
> 따라서 √n 이하의 소수로 나누어 떨어지지 않으면 그 수는 소수이다.

### 소수 3 (여러 개의 소수 판별(flag, for-break-else))

```py
loop = int(input())
unchecked_list = list(map(int,input().split()))

prime_count = 0
for i in unchecked_list:
    if i < 2:
          continue
    for j in range(2, int(i**(1/2))+1):
        if i % j == 0:
            break
    else: 
          prime_count += 1

print(prime_count)
```

```py
unchecked_list = list(map(int,input().split()))

prime_count = 0
for i in unchecked_list:
    if i < 2:
        continue
    is_prime = True
    for j in range(2,int(i**(1/2)+1)):
        if i % j == 0:
            is_prime = False
            break

    if is_prime:                 #소수로 판별되어 내부For문이 break가 되도, 밑에 있는 문장은 외부 For문이므로 반드시 실행됨. 
        prime_count += 1         #그러므로 is_prime = False 로 플래그 변수를 만든다.

print(prime_count)
```


### 팩토리얼(재귀)

```py
def factorial(n):
  if n == 1:
     return 1
  while n!=0:
     retrun n*factorial(n-1) 
     
```
> 반드시 **if n==1 처럼 종료 조건을 만드는 것이 중요**하다.  
