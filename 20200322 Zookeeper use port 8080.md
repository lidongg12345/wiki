##20200322 Zookeeper use port 8080

    Today, when I start zookeeper3.6.0, failed, view the logs:
        org.apache.zookeeper.server.admin.AdminServer$AdminServerException: Problem starting AdminServer on address
         0.0.0.0, port 8080 and command URL /commands
        	at org.apache.zookeeper.server.admin.JettyAdminServer.start(JettyAdminServer.java:176)
        	at org.apache.zookeeper.server.ZooKeeperServerMain.runFromConfig(ZooKeeperServerMain.java:153)
        	at org.apache.zookeeper.server.ZooKeeperServerMain.initializeAndRun(ZooKeeperServerMain.java:112)
        	at org.apache.zookeeper.server.ZooKeeperServerMain.main(ZooKeeperServerMain.java:67)
        	at org.apache.zookeeper.server.quorum.QuorumPeerMain.initializeAndRun(QuorumPeerMain.java:140)
        	at org.apache.zookeeper.server.quorum.QuorumPeerMain.main(QuorumPeerMain.java:90)
        Caused by: java.io.IOException: Failed to bind to /0.0.0.0:8080
        	at org.eclipse.jetty.server.ServerConnector.openAcceptChannel(ServerConnector.java:346)
        	at org.eclipse.jetty.server.ServerConnector.open(ServerConnector.java:307)
        	at org.eclipse.jetty.server.AbstractNetworkConnector.doStart(AbstractNetworkConnector.java:80)
        	at org.eclipse.jetty.server.ServerConnector.doStart(ServerConnector.java:231)
        	at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:72)
        	at org.eclipse.jetty.server.Server.doStart(Server.java:385)
        	at org.eclipse.jetty.util.component.AbstractLifeCycle.start(AbstractLifeCycle.java:72)
        	at org.apache.zookeeper.server.admin.JettyAdminServer.start(JettyAdminServer.java:167)
        	... 5 more
        Caused by: java.net.BindException: Address already in use
        	at sun.nio.ch.Net.bind0(Native Method)
        	at sun.nio.ch.Net.bind(Net.java:433)
        	at sun.nio.ch.Net.bind(Net.java:425)
        	at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
        	at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
        	at org.eclipse.jetty.server.ServerConnector.openAcceptChannel(ServerConnector.java:342)
        	... 12 more
    The reason is begin 3.5.0, Zookeeper included jetty, used port 8080 to listen:
        [The AdminServer].(https://zookeeper.apache.org/doc/r3.6.0/zookeeperAdmin.html#sc_adminserver)
    We can use the follow config:
        New in 3.6.0: The following options are used to configure the AdminServer.
            admin.portUnification : (Java system property: zookeeper.admin.portUnification) Enable the admin port to accept both HTTP and HTTPS traffic. Defaults to disabled.
        New in 3.5.0: The following options are used to configure the AdminServer.
            admin.enableServer : (Java system property: zookeeper.admin.enableServer) Set to "false" to disable the AdminServer. By default the AdminServer is enabled.
            admin.serverAddress : (Java system property: zookeeper.admin.serverAddress) The address the embedded Jetty server listens on. Defaults to 0.0.0.0.
            admin.serverPort : (Java system property: zookeeper.admin.serverPort) The port the embedded Jetty server listens on. Defaults to 8080.
            admin.idleTimeout : (Java system property: zookeeper.admin.idleTimeout) Set the maximum idle time in milliseconds that a connection can wait before sending or receiving data. Defaults to 30000 ms.
            admin.commandURL : (Java system property: zookeeper.admin.commandURL) The URL for listing and issuing commands relative to the root URL. Defaults to "/commands".
    So, we can vi zoo.cfg, if you no need, you can:
        admin.enableServer=false
    if you want to change port, you can:
        admin.serverPort=8088