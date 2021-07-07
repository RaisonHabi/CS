## 利用pandas包
示例：  
> import pandas as pd  
#任意的多组列表  
a = [1,2,3]  
b = [4,5,6]       
#字典中的key值即为csv中列名  
dataframe = pd.DataFrame({'a_name':a,'b_name':b})  
#将DataFrame存储为csv,index表示是否显示行名，default=True  
dataframe.to_csv("test.csv",index=False,sep=',')  
结果：  
   a_name  b_name  
0       1       4  
1       2       5  
2       3       6  

## pandas也提供简单的读csv方法
示例：  
> import pandas as pd  
data = pd.read_csv('test.csv')  

得到一个DataFrame类型的data
## 用csv包，一行行写入
示例：  
> import csv  
#python2可以用file替代open  
with open("test.csv","w") as csvfile:   
  writer = csv.writer(csvfile)  
  #先写入columns_name  
  writer.writerow(["index","a_name","b_name"])  
  #写入多行用writerows  
  writer.writerows([[0,1,3],[1,2,3],[2,3,4]])  
结果：  
index   a_name  b_name  
0       1       3  
1       2       3  
2       3       4  
## 读取csv文件用reader
示例：  
> import csv  
with open("test.csv","r") as csvfile:  
    reader = csv.reader(csvfile)  
    #这里不需要readlines  
    for line in reader:  
        print line  
        
 [python写入csv文件的几种方法总结](https://blog.csdn.net/waple_0820/article/details/70049953)
