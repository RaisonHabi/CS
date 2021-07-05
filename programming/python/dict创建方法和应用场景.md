## dict()
字典是Python中唯一键值映射类型，该类型在处理大数据量的效率，比列表，元祖高的多。  
字典的创建方法有很多，根据不同的场景创建字典，很有讲究，也可以让我们编程更加便利！
### 0、dp Dynamic programming  中的备忘录
[动态规划详解进阶](https://labuladong.github.io/ebook/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%B3%BB%E5%88%97/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E8%AF%A6%E8%A7%A3%E8%BF%9B%E9%98%B6.html)
```
def coinChange(coins: List[int], amount: int):
    # 备忘录
    memo = dict()
    def dp(n):
        # 查备忘录，避免重复计算
        if n in memo: return memo[n]

        if n == 0: return 0
        if n < 0: return -1
        res = float('INF')
        for coin in coins:
            subproblem = dp(n - coin)
            if subproblem == -1: continue
            res = min(res, 1 + subproblem)

        # 记入备忘录
        memo[n] = res if res != float('INF') else -1
        return memo[n]

    return dp(amount)
```
实验
```
mem=dict()
mem[0]=1
mem[1]=1
print(mem)
{0: 1, 1: 1}
```

&nbsp;
### 常见方式
#### 方式一: 直接创建
```
>>> D1 = {'name': 'Tom', 'age': 40}           # 直接创建
>>> D1                                        # 适用场景: 事先已经拼接出整个字典
{'age': 40, 'name': 'Tom'}
```
#### 方式二: 动态创建
```
>>> D2 = {}                                   # 动态创建
>>> D2['name'] = 'Tom'                        # 动态赋值
>>> D2['age'] = 40		              # 动态赋值
>>> D2                                        # 适用场景: 适用于动态创建字典的一个字段
{'age': 40, 'name': 'Tom'}
```
#### 方式三: 关键字创建
```
>>> D3 = dict(name='Tom', age=40)             # 关键字创建
>>> D3                                        # 适用场景: 关键字形式所需的代码比常量少，但键必须为字符串
{'age': 40, 'name': 'Tom'}
```
#### 方式四: 键/值对创建
```
>>> D4 = dict((['name', 'Tom'], ['age', 40])) # 键值对创建
>>> D4                                        # 适用场景: 需要把键值逐步建成序列，此形式比较适用
{'age': 40, 'name': 'Tom'}
```
#### 方式五: 初始化字典
```
>>> D5 = dict.fromkeys(['a', 'b'], 0)         # 初始化字典
>>> D5                                        # 适用场景: 所有键的值都相同，此形式非常适用
{'a': 0, 'b': 0}
```
#### 方式六: zip创建字典
```
>>> D6 = dict(zip(['a', 'b'], [1, 2]))        # zip创建
>>> D6                                        # 适用场景: 创建键列表和值列表，适用此方式比较适合
{'a': 1, 'b': 2}
```
#### 方式七: 通过字典解析来创建字典
```
>>> # 通过字典解析来创建字典
>>> # 适用场景: 动态，灵活地来创建字典
>>> # 示例一:
>>> D = {k:0 for k in 'ab'}
>>> D
{'a': 0, 'b': 0}
>>> # 示例二:
>>> D = {k:v for (k,v) in zip(['a', 'b'], [1, 2])}
>>> D
{'a': 1, 'b': 2}
>>> # 示例三:
>>> D = {k: ord(k) for k in ['A', 'B', 'C', 'D']}
>>> D
{'A': 65, 'C': 67, 'B': 66, 'D': 68}
>>> # 示例四:
>>> D = {c.lower(): c + '!' for c in ['SPAM', 'EGGS', 'HAM']}
>>> D
{'eggs': 'EGGS!', 'ham': 'HAM!', 'spam': 'SPAM!'}
```

&nbsp;
## References
[Python中字典创建的几种方法及适用场景](https://blog.csdn.net/Jerry_1126/article/details/78239530)
