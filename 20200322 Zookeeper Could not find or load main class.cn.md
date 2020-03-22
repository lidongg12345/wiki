#Zookeeper Could not find or load main class org.apache.zookeeper.server.quorum

    出现该问题时，是因为下载的版本不正确，正确的版本为xxx-3.6.0-bin.tar.gz；
    当时正准备在官网下这个文件，但下载速度实在太慢，便去zookeeper的git的releases下载了release-3.6.0.tar.gz；
    正常解压后，改完了zoo.cfg，然后去启动，结果提示启动失败，进程也没启动起来，查看日志时，提示了这个错误：
        Could not find or load main class org.apache.zookeeper.server.quorum
    经查询得知，我下载的压缩包为源码包，真正执行时，还需要额外的库，而bin包才是可直接执行的版本，重新下载后，问题解决。