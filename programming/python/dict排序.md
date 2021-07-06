## 按key排序
sorted(iterable,key,reverse)  
> iterable表示可以迭代的对象，例如可以是dict.items()、dict.keys()等;  
**key是一个函数，用来选取参与比较的元素**;  
reverse则是用来指定排序是倒序还是顺序，reverse=true则是倒序，reverse=false时则是顺序，默认时reverse=false。

另，***直接使用sorted(d.keys())就能按key值对字典排序***
## 按value值对字典排序
要对字典的value排序则需要用到key参数  
这里提供一种使用lambda表达式的方法：
> imp_map_new = sorted(imp_map.items(),**key=lambda item:item[1]**,reverse=True)

items()方法将字典的元素转化为了元组  
而这里key参数对应的lambda表达式的意思则是选取元组中的第二个元素作为比较参数  
如果写作key=lambda item:item[0]的话则是选取第一个元素作为比较对象，也就是key值作为比较对象。  
lambda x:y中x表示输出参数，y表示lambda函数的返回值，所以采用这种方法可以对字典的value进行排序。  
注意排序后的返回值是一个list，而原字典中的键值对被转换为了list中的元组。
