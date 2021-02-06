---
title: Bisection Search
date: 2020-02-05
---

## MIT 二分探索方
2% for annual rate on the balance per year  
$3329 is the balance

**the minimum fixed monthly payment needed in order pay off a credit card balance within 12 months**

## My answer without using the bisection search
```python
balance = 3329
annualInterestRate = 0.2
          

def remainingBalance(remaining, lowestPayment, annualRate, month, defaultBalance):
    unpaid     = remaining - lowestPayment
    interest   = (annualRate / 12) * unpaid
    
    new_unpaid = unpaid + interest
    
    if month < 11:
        remainingBalance(new_unpaid, lowestPayment, annualRate, month + 1, defaultBalance)
    
    if month == 11 and new_unpaid > 0:
        remainingBalance(defaultBalance, lowestPayment + 10, annualRate, 0, defaultBalance)
        
    if month == 11 and new_unpaid < 0:
        print(lowestPayment)


remainingBalance(balance, 10, annualInterestRate, 0, balance)
```

## with Bisectin Search
今回の問いでは二分探索方を利用するのだが、前回の問いのように$10から初めて、残高が0になるまでを繰り返すのは冗長である。  
その為、最大値と最低値を設定した方が時間を短くすることができる。  
最低値は簡単に求めることができる。  
例えば1200ドルの借金がある場合、1年で決済するのであれば、毎月100ドルは最低でも返済しなければいけない。  
最大値は、借金額に年会費を足したものを12で割ったものになる。理由としては、年会費を1年の最後に支払ったとしても、最大値は借金額に2%を足したものになるからである。極論を言えば、最大値が年会費+借金額($1440)を超えることはないから。
なので、二分探索方を用いる場合、$100 ~ $120の間で探索すればいい。


```python
balance = 999999
annualInterestRate = 0.18

def paymentBoudsGenerator(min, max):
    ary: list[float] = []
    
    while min <= max:
        ary.append(min)
        min += 0.01
        
    return ary


def isPaidOff(monthly_payment, balance, annualRate):
    remain = balance - monthly_payment
    paid = balance - remain
    
    for i in range(11):
        paid += monthly_payment
        interest = (annualRate / 12) * remain
        remain = (remain + interest) - monthly_payment
            
        if i == 10:
            if remain > 0.1:
                return 'less'
            
            if remain < -0.1:
                return 'much'
            
            if 0.1 > remain > -0.1:
                return True
        
        i += 1


def balanceBisectionSearch(balance: int, annualRate: float):
    monthly_rate:    float = annualRate / 12
    maximum_payment: float = (balance * (1 + monthly_rate)**12) / 12
    minimum_payment: float = balance / 12
    
    bounds: list[int] = paymentBoudsGenerator(minimum_payment, maximum_payment)
    
    head: int = 0
    tail: int = len(bounds) - 1
    
    while head <= tail:
        center: int = (head + tail) // 2
        
        result = isPaidOff(bounds[center], balance, annualRate)
        
        if result == True:
            return print('Lowest Payment: ' + str(round(bounds[center], 2)))
        
        if result == 'much': tail = center -1;
        if result == 'less': head = center + 1;
            

        
balanceBisectionSearch(balance, annualInterestRate)
```
