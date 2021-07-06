## pop()
**描述**  
pop() 函数用于移除列表中的一个元素（默认最后一个元素），并且返回该元素的值。  
**语法**  
pop()方法语法：  
list.pop([index=-1])  
**参数**  
obj -- 可选参数，要移除列表元素的索引值，不能超过列表总长度，***默认为 index=-1，删除最后一个列表值***。  
**返回值**  
该方法返回从列表中移除的元素对象。  
实例:  
> list1 = ['Google', 'Runoob', 'Taobao']  
list_pop=list1.pop(1)  
print "删除的项为 :", list_pop  
print "列表现在为 : ", list1  
以上实例输出结果如下：  
删除的项为 : Runoob  
列表现在为 :  ['Google', 'Taobao']  

## map()
**map(function, iterable, …)**  
返回一个列表  
参数：
> 参数function传的是一个函数名，可以是python内置的，也可以是自定义的。   
参数iterable传的是一个可以迭代的对象，例如列表，元组，字符串这样的。

示例：  
> a=(1,2,3,4,5)  
b=[1,2,3,4,5]  
c="zhangkang"  
la=map(str,a)  
lb=map(str,b)  
lc=map(str,c)  
print(la)  
print(lb)  
print(lc)  
输出：  
['1', '2', '3', '4', '5']  
['1', '2', '3', '4', '5']  
['z', 'h', 'a', 'n', 'g', 'k', 'a', 'n', 'g']  

***str()是python的内置函数，这个例子是把列表/元组/字符串的每个元素变成了str类型，然后以列表的形式返回。***    
当然我们也可以传入自定义的函数。

## extend()
**描述**  
extend() 函数用于在列表末尾***一次性追加另一个序列中的多个值***（用新列表扩展原来的列表）。  
**语法**  
list.extend(seq)  
**参数**  
seq -- 元素列表。  
**返回值**  
该方法没有返回值，但会在已存在的列表中添加新的列表内容。  
**实例**  
aList = [123, 'xyz', 'zara', 'abc', 123]  
bList = [2009, 'manni']  
aList.extend(bList)  
print ("Extended List : ", aList)  
以上实例输出结果如下：  
Extended List :  [123, 'xyz', 'zara', 'abc', 123, 2009, 'manni']
