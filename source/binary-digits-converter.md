## just an example of how you convert decimal digits to binary digits

```pytho
num = 3
result = ''

if num < 0:
    isNeg = True
else:
    isNeg = False
    

if num == 0:
    result = '0'

while num > 0:
    result = str(num % 2) + result
    num = num // 2
    
if isNeg:
    result = '-' + result
    
print(result)
```

## a solution for fractions
```python
x = float(input('Enter a decimal number between 0 and 1: '))
p = 0
while ((2**p) *x) %1 != 0:
    # 整数との差が01になるまで繰り返し
    print('Remainder = '+ str((2**p) *x - int((2**p) *x)))
    p += 1

num = int(x* (2**p))

result = ''

if num == 0:
    result = '0'
    
while num > 0:
    # 2進数なので割り切った余りが1 or 0で判定
    result = str(num%2) + result
    print(num)
    num = num // 2
    
for i in range(p - len(result)):
    result = '0' + result
    

result = result[0:-p] + '.' + result[-p:]
print('The binary representation of the decimal !' + str(x) + ' is ' + str(result))
```
