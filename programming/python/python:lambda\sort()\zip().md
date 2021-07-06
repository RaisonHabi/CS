
## lambda语法格式  
**lambda [arg1 [, agr2,.....argn]] : expression**  
*Python中，lambda函数也叫匿名函数，及即没有具体名称的函数，它允许快速定义单行函数，类似于C语言的宏，可以用在任何需要函数的地方。
这区别于def定义的函数。*   
*示例：*  
>1、单个参数的：  
> g = lambda x : x ** 2  
> print g(3)  
9  
2、多个参数的：  
> g = lambda x, y, z : (x + y) ** z  
> print g(1,2,2)  
9    

## sort() sorted()  
**sort()方法可以直接修改列表**  
**sorted()会从一个可迭代对象构建一个新的排序列表**  
***list.sort() 方法只是为列表定义的，而 sorted() 函数可以接受任何可迭代对象***  
示例1：   
> a = [5, 2, 3, 1, 4]  
> a.sort()  
> a  
[1, 2, 3, 4, 5]  

示例2:  
> student_tuples = [('john', 'A', 15),('jane', 'B', 12),('dave', 'B', 10)]  
print(sorted(student_tuples,key=lambda st:st[2],reverse=True))  
[('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]  

示例3:  
> test=('D','a','g')  
print(sorted(test,***key=str.lower***))  
['a', 'D', 'g']

## zip()  
描述：用于将可迭代的对象作为参数，将对象中对应的元素打包成***一个个元组***，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。  
*注1：如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同*  
*注2:zip 方法在 Python 2 和 Python 3 中的不同：在 Python 3.x 中为了减少内存，zip() 返回的是一个对象。如需展示列表，需手动 list() 转换。*  
**利用 * 号操作符，可以将元组解压为列表。**      
示例：  
> a = [1,2,3]  
b = [4,5,6]  
 c = [4,5,6,7,8]  
 zipped = zip(a,b)           # 返回一个对象    
 print(zipped)    
<zip object at 0x103abc288>  
list(zipped)                 # list() 转换为列表   
[(1, 4), (2, 5), (3, 6)]   
 list(zip(a,c))              # 元素个数与最短的列表一致  
[(1, 4), (2, 5), (3, 6)]  

> a1, a2 = zip(\*zip(a,b))     # 与 zip 相反，zip(\*) 可理解为解压，返回二维矩阵式  
print(list(a1))  
[1, 2, 3]  
print(a1)  
(1,2,3)  
print(list(a2))  
[4, 5, 6]
