##Zookeeper Could not find or load main class org.apache.zookeeper.server.quorum

    This problem, because the package I have downloaded is incorrect. The correct package is xxx-3.6.0-bin.tar.gz;
    Today, I was preparing to download the bin package on the official website, but the speed was too slow(as you know), so I went to git's releases of zookeeper to download the release-3.6.0.tar.gz;
    After the normal decompression, update zoo.cfg and start it. The result indicates that the startup failed and the process did not start. When I viewed the log, this error is prompted:
        Could not find or load main class org.apache.zookeeper.server.quorum
    After query, we know that the compressed package I downloaded is the source package. When it is actually executed, additional libraries are needed, and bin package is the directly executable version. After downloading bin again, the problem is solved.