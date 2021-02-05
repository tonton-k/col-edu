---
title: Say Hello to the world
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

## Useful links

- Website: https://gitpress.io
- Getting Started: https://gitpress.io/c/help/welcome
