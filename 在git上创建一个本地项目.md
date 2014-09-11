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

<pre><code>git clone https://github.com/yangrong/fortext.git·</code></pre>

这里的url是在我们创建仓库的时候生成的那个链接。

这样我们就把本地的指定文件夹跟github关联上了。


我们可以在d盘上面找到如下图标就是我们拉下来的仓库文件

![alt text](http://p2.qhimg.com/t01cf0e7ed3d52e013f.png)

如果我们本地代码文件，往本地仓库文件上扔，然后要上传到github上面，需要执行如下步骤：

在fortext的文件上（就是拉下来的仓库文件）右键，选择git bash

执行命令
<pre><code>
git pull 
git add （需要添加的文件）
git commit -m ''
git push
</code></pre>

其他git命令：

<pre><code>Git status</code></pre>

查看当前文件状态 如果有文件有改动会显示如图

![alt text](http://p5.qhimg.com/t0105fa3589f66a8bcd.png)

显示 localStorage.html 有修改的地方。

如果上面改过的这个文件，在线上代码仓库修改，那么照常执行

<pre><code>
git add （需要添加的文件）
git commit -m ''
git pull 
git push
</code></pre>
这样是push不上去的，因为线上线下有冲突，在执行git pull 的时候，会有如下的提示
![alt text](http://p6.qhimg.com/t0121d600ff52c01880.png)

这里我打开本地代码文件，在冲突的代码，解决冲突，如图，解决下面的冲突
![alt text](http://p6.qhimg.com/t0195f271687b18494f.jpg)

然后直接
再执行
<pre><code>
git pull 
git add （需要添加的文件）
git commit -m ''
git push
</code></pre>
这样就可以把解决完冲突的文件push到线上去了。

