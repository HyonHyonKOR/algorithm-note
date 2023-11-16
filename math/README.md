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
