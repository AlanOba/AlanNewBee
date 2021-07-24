# Mac显示隐藏文件的方法

Mac下默认Finder是不显示隐藏文件的，譬如maven的.m2文件夹，那时我想做的操作是想把.m2文件夹拷到硬盘里，然后Finder无法操作，我又转到命令行模式，命令行下ls -a是可以看到隐藏文件的，但是，我命令行下压缩这个.m2文件夹，死活不让我压缩，So最后放弃了压缩复制的念头。

后面只能网finder方向查找显示隐藏文件的方法，最后解决如下：

进入终端，输入命令行

```
defaults write com.apple.finder AppleShowAllFiles FALSE 
defaults write com.apple.finder AppleShowAllFiles TRUE
```



2.还需要在终端中调用 `killall Finder` 重启 Finder 才能应用修改。

![img](https://img-blog.csdn.net/20171031143234472?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjU1NzUzOA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)