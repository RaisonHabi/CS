## 读
.CSV文件是以逗号分割的数据仓储，读取数据时从每一行中读取一条数据元祖，也就是一条数据，再用字符分割的方式获取表中的每一个数据项。

    import java.io.BufferedReader;   
    import java.io.FileReader;   
    
    public class TestRead {   
        public static void main(String[] args) {   
            try {   
                BufferedReader reader = new BufferedReader(new FileReader("a.csv"));//换成你的文件名  
                reader.readLine();//第一行信息，为标题信息，不用，如果需要，注释掉  
                String line = null;   
                while((line=reader.readLine())!=null){   
                    String item[] = line.split(",");//CSV格式文件为逗号分隔符文件，这里根据逗号切分  
                     
                    String last = item[item.length-1];//这就是你要的数据了  
                    //int value = Integer.parseInt(last);//如果是数值，可以转化为数值  
                    System.out.println(last);   
                }   
            } catch (Exception e) {   
                e.printStackTrace();   
            }   
        }   
    
    }  
    
## 写
写入数据则注意数据逗号分隔的格式，以文件写入的方式即可。

    package com.mark.csv;   
    
    import java.io.BufferedWriter;   
    import java.io.File;   
    import java.io.FileNotFoundException;    
    import java.io.FileWriter;   
    import java.io.IOException;   
    
    public class WriteCSV {   
    
      public static void main(String[] args) {   
        try {   
          File csv = new File("F:/writers.csv"); // CSV数据文件  
    
          BufferedWriter bw = new BufferedWriter(new FileWriter(csv， true)); // 附加  
          // 添加新的数据行
          bw.write(""李四"" + "，" + ""1988"" + "，" + ""1992"");   
          bw.newLine();   
          bw.close();   
    
        } catch (FileNotFoundException e) {   
          // File对象的创建过程中的异常捕获  
          e.printStackTrace();   
        } catch (IOException e) {   
          // BufferedWriter在关闭对象捕捉异常  
          e.printStackTrace();   
        }   
      }   
    }  
  
&nbasp;
## References
[Java从.CSV文件中读取数据和写入](https://www.cnblogs.com/leihupqrst/p/3508410.html)
