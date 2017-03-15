

###写在前面###
	这是我在使用AS中关于Gradle遇过的一些坑,总结出来供大家参考交流,声明这是一篇技(傻)术(瓜)文(干)章(货),大神请绕道,里面讲的一些可能你们早
	已掌握或有更好的解决方法 --->  下面让我们进入正题
###AS导入项目###
	 当我们从Github上或者朋友那拿到一个项目,然后在导入项目的时候就遇到下面图片上的情况,无法加载有木有,连个进度都没有,而且只能从后台杀死AS.
![无法加载项目,并且只能后台强制杀死](http://img.blog.csdn.net/20170304141733114?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
AS采用Gradle来编译项目相信大家都十分清楚,问题就出在这里.因为在首次导入项目的时候AS默认是使用gradle-wrapper-properties中默认的设
置,它会从网上下载所需要的对应版本的gradle,因为该网址的服务器在国外,虽然没有被墙掉,但是由于网络十分不稳定,所以一般不会下载成功,所以
你永远无法导入你的项目.
###解决方法一###
因为是联网操作,所以那就简单粗暴一点,断掉电脑所有的网络.这是你会发现导入界面一闪而过来到熟悉的编辑界面,先不要开心的太早.这里导入的
项目还是没有经过build的 --->这是你所需要做的 ---> 打开AS设置,具体在哪了?我也不知道,快捷键 ctrl+alt+s,在搜索框输入gradle会出现下面这
个界面![这里写图片描述](http://img.blog.csdn.net/20170304145236615?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
蓝色的默认选项去掉,勾选选用本地和离线工作时的的gradle,
accept ---> ok ---> 恢复网络 ---> syncproject一般情况下就不会再出现任何问题,编译成功
###解决方法二###
断网,不想有没有,那还有解决的方法没有,当然有.在你的项目中找到gradle-wrapper-properties这个文件,把最后一行的网址删除注释等等,
反正就是让它无法连接该网址,剩余步骤请参考方法一.
##gradlehome##
可能在方法一方法二中你们在设置的时候本地和网络上面的文件选项都是空的,不知道gradle在哪?来吧,因为只有设置过gradlehome它才会自动选
目录择 ---> 上图
![这里写图片描述](http://img.blog.csdn.net/20170304150627293?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
环境变量的配置 -->我的电脑-->高级系统设置-->环境变量
先配置gradlehome
![这里写图片描述](http://img.blog.csdn.net/20170304150817622?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
在配置path
![这里写图片描述](http://img.blog.csdn.net/20170304150933669?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

这样再次打开AS中gradle配置的时候就可以自动获取相匹配的gradle版本了,觉得到这里就完了,不!!!来下载一把gradle爽爽;
###Gradle下载###
强迫症有没有,总觉得用自己的gradle有点不靠谱,没有和大神的用的版本一致,会不会出问题,心慌慌,下面我就分享一下自己下载gradle的经验.

![这里写图片描述](http://img.blog.csdn.net/20170304152147765?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
因为在国内访问国外的服务器,如果你无法科学上网,肯定无法下载成功,但又要下载,就很矛盾,本人亲测,下载也不是不可以,但你需要使用下载器,因为
可以断点续传 --->走正题
首先还是得找到这个文件gradle-wrapper-properties!将具体的版本的gradle号替换,复制该网址到下载器或者游览器,等待下载,可能会有点慢
需要耐心等待  下载结束,恭喜你第一步完成;
第二步:
使用Tomcat服务器自己搭载下载链接,将下载好的文件放到
![这里写图片描述](http://img.blog.csdn.net/20170304153136086?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
第三步:
使用游览器测试一下自己的服务器网址是否可用
![这里写图片描述](http://img.blog.csdn.net/20170304153428361?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
记得别忘开服务器,如果没有comcat请自行百度,相信我很简单!
第四步:
重点来了将上面的网址替换gradle-wrapper-properties里面的网址!
![这里写图片描述](http://img.blog.csdn.net/20170304153928637?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
然后去设置中改用默认的gradle (方法一中绿色勾上,红色去掉)---> 关闭AS ---> 正常打开项目 ,这里最好在project 中删除该项目;
神奇的事情就可以发生了,等待它下载好,然后它自己就可以自动解压;不用你去官网找资源被英语各种虐,也不用在官网下载好然后不知道解压到哪?
一切就是这么简单.
##结后语##
这样还有二个坑不知怎么解决
一 : 虽然这样设置过可以解决导入不了项目的问题,但是每次导入都得重新设置一遍,很痛苦!!!现在没有找到解决办法,希望大神指教.
二 : 当设置过gradlehome 后下载gradle的时候会下载到你想象不到的目录下,上图按道理应该下载到这个目录![这里写图片描述](http://img.blog.csdn.net/20170304155150408?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
可实际它会下载到你设置的gradlehome的文件夹下面
![这里写图片描述](http://img.blog.csdn.net/20170304155425607?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3R1ZHlfQWJj/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
原因是gradle-wrapper-properties的配置文件里面的文件路径的配置问题,目前本人还没解决,你可以手动的把它放到该放的目录,亲测可以使用!
希望给大家带来一些方便.




