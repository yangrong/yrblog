#### 在git上创建一个本地项目

###### 首先在github上面创建一个仓库
如图：

![alt text](http://p0.qhimg.com/t0125db2260c7093cbd.png)

创建完毕之后，会生成一个链接

![alt text](http://p3.qhimg.com/t01f67fdc460834b91c.png)

然后再本地的git Bash

cd (你要把代码仓库放在哪个路径下面，比如 d: ,就是放在d盘下面) 

执行命令 cd d：

然后执行clone命令，把github的仓库clone到本地

·git clone https://github.com/yangrong/fortext.git·

这里的url是在我们创建仓库的时候生成的那个链接。

这样我们就把本地的指定文件夹跟github关联上了。


我们可以在d盘上面找到如下图标就是我们拉下来的仓库文件

![alt text](http://p2.qhimg.com/t01cf0e7ed3d52e013f.png)

如果我们本地代码文件，往本地仓库文件上扔，然后要上传到github上面，需要执行如下步骤：

在fortext的文件上（就是拉下来的仓库文件）右键，选择git bash

执行命令
·
git pull 

git add （需要添加的文件）

git commit -m ''

git push
·



