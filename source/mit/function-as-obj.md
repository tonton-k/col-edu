# One of the interesting way to handle function

you just need to simply pass a list which holds functions of what you wanna to do to the list you provide

```python
def applyFuncs(funcList, list):
    
    for F in funcList:
        list = [ F(i) for i in list ]
        print(list)
        
    
    
funcList = [abs, int, bin]
nums = [3.5, 10, 4]

applyFuncs(funcList, nums)

```
