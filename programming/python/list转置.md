**示例：**  
> a = [[1,2,3], [4,5,6]]  
print (a)  
print (map(list, zip(*a)))  
print (list(map(list, zip(*a))))

注：第三行在python3中输出结果为<map object at 0x036D04F0>

因为版本问题，改为第四行即可，否则得到结果为map对象
