# CCA131
Important information about the topics covered in CCA131

Enabling Load Balancing and High Availability for Hiveserver2

Step 1 - Add multiple Hiveserver2 role instance (more than 2) and start them.

Step 2 - Open Hive -> Configuration -> Category -> Advanced.
Find “HiveServer2 Advanced Configuration Snippet (Safety Valve) for hive-site.xml”
Add a new property as below:
Name: hive.server2.support.dynamic.service.discovery
Value: true

Step 3 - Restart hive service and redeploy configuration

Step 4 - SSH to any data node. Connect to Hiveserver2 using Beeline.
# beeline 

# beeline> !connect jdbc:hive2://ip-of zookeeper instance1:2181,ip-of zookeeper instance2:2181,ip-of zookeeper instance3:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2

For eg:

beeline> !connect jdbc:hive2://machine1.local.com:2181,machine2.local.com:2181,machine3.local.com:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2
scan complete in 1ms
Connecting to jdbc:hive2://machine1.local.com:2181,machine2.local.com:2181,machine3.local.com:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2
Enter username for jdbc:hive2://machine1.local.com:2181,machine2.local.com:2181,machine3.local.com:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2:
Enter password for jdbc:hive2://machine1.local.com:2181,machine2.local.com:2181,machine3.local.com:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2:
18/11/14 02:52:39 [main]: INFO jdbc.HiveConnection: Connected to machine2.local.com:10000
Connected to: Apache Hive (version 1.1.0-cdh5.15.1)
Driver: Hive JDBC (version 1.1.0-cdh5.15.1)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://machine1.local.com:2181,machi>

