## 步骤

利用git从一个仓库拷贝一个项目到另一个仓库，并且log也迁移过去
 
```
1 先从原地址clone一份代码到本地
 
git clone --bare http://github....(原始仓库地址)
 
2  进入克隆下来的目录
 
3 以镜像推送的方式上传代码到新的仓库地址
 
git push --mirror http：//...(目标仓库地址)
```

&nbsp;
## References
[从一个git仓库拷贝到另一个git仓库](https://blog.csdn.net/m0_37714008/article/details/111246264)
