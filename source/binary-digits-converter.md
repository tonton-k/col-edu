## just an example of how you convert decimal digits to binary digits

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
