## str(),eval()
### 字符串转换为字典：
```
str_test = "{'a': 1, 'b': 2}"
dict_test = eval(str)
```
### 字典转换为字符串：
```
dict_test = {'a': 1, 'b': 2}
str_test = str(dict)
```
### eval() 函数
eval() 函数用来执行一个字符串表达式，并返回表达式的值。

eval(expression[, globals[, locals]])
参数
```
expression -- 表达式。
globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。
```
实例
```
以下展示了使用 eval() 方法的实例：

>>>x = 7
>>> eval( '3 * x' )
21
>>> eval('pow(2,2)')
4
>>> eval('2 + 2')
4
>>> n=81
>>> eval("n + 4")
85

print(eval("{'a':1,'b':2}"))
{'a': 1, 'b': 2}
```
### pow() 函数
pow() 方法返回 xy（x的y次方） 的值。

#### 以下是 math 模块 pow() 方法的语法:
```
import math

math.pow( x, y )
```
#### 内置的 pow() 方法
pow(x, y[, z])
函数是计算x的y次方，如果z在存在，则再对结果进行取模，其结果等效于pow(x,y) %z

#### 注意：pow() 通过内置的方法直接调用，内置方法会把参数作为整型，而 math 模块则会把参数转换为 float。

&nbsp;
## References
[python中字符串和字典类型互相转换](https://blog.csdn.net/bcfdsagbfcisbg/article/details/78276686)
