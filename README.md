                                        #对git的安装及其使用心得
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天在thoughtworker 老师的带领下我学习及安装使用git这个软件，期间经历过无数次困难与挫折，
 我想把我所遇到的问起及解决方法告诉给大家，供大家参考学习。<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;使用给git之前最好先建议不要健在好home目录下最好也不要建在桌面，应该先建一个projects目录下面在建一个目录。
如果你此前已经犯了上面的错误，不要想着卸载git这是行不通的，要进入git所在的目录，注意使用ls -al查看，因为。
git目录默认是隐藏文件，如果在桌面上，你发现你执行了rm -rf .git文件发现图标依旧在，请关机重启。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;接下来我们需要配置git的环境.1打开https://github.com/ 2.点击help 3.点击 set up git.执行一下命令：<p>
（1）git config --global user.name "YOUR NAME"     //填写你的用户名。
（2）git config --global user.email "YOUR EMAIL ADDRESS"    //填写你的电子邮箱 
接下来配置ssh.
在上个页面上找Connecting over SSH点击generate SSH keys将进入ssh的配置页面。执行一下命令配置ssh.
(1)ls -al ~/.ssh
(2)ssh-keygen -t rsa -C "your_email@example.com"   //填写你的电子邮箱地址
(3)eval "$(ssh-agent -s)"
(4)ssh-add ~/.ssh/id_rsa
(5)sudo apt-get install xclip
(6)xclip -sel clip < ~/.ssh/id_rsa.pub
接下来回到github.com.在你点击用户名右边第三个按钮设置ssh点击ssh.把生成的连接黏贴进去，
使用ssh连接以后如果以后上传修改文件就方便多啦．
在github上，上传文件有两种方式，第一种可以直接写好以后黏贴到github的网页上，（不建议使用）第二种方式就是下载以Atom软件。
点击加号创建工程，然后创建git库，输入git init。
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;连接atom,输入 atom README.md接着执行下面命令
git add README.md   //将add README.md添加到缓存区
git commit -m "first commit"  //第一次进行提交
git remote add origin git@github.com:Springwlt/LuckStatr1.git  //把git与git的远程服务台连接
git push -u origin master   //进行提交
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通过 git add 文件名命令 可以把文件加入到缓存区，通过git status 命令 可以查看缓存去的内容，通过 git commit -a -m "说明"
命令，可以一次行添加多个文件，“说明”主要是加注释的，可有可无。<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下面我介绍一下学习git的两个网站：This is an http://try-git.codefordream.com/（中文版） This is an https://try.github.io/levels/1/challenges/1（英文版）　
