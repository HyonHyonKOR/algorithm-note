# 알고리즘 노트(파이썬)


### 약수 

```python

n = 9

arr = []

for i in range(1,int(n**(1/2))+1) :
  if n % i == 0: 
      arr.append(i) 
      if i**2 !=n: 
          arr.append(n//i)

print(arr) # 약수 리스트
print(len(arr)) # 약수의 갯수 
```

### 소수 판별

```python
def is_prime_number(n):
    if n < 2:
        return False
    for i in range(2, int(n**(1/2)) + 1):
        if n % i == 0:
            return False
    return True
```

### 여러 개의 소수 판별(for-break-else)

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


     
  
