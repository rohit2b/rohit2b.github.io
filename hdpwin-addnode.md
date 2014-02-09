# Guide: Adding a slave node to an existing HDP for Windows cluster.

This guide was developed for HDP 2.0 for Windows. The commands and steps were 
carried out on a Windows Server 2012 R2 set of machines.

### Start with an existing HDP for Windows cluster

For this guide, I've started with a single node HDP 2.0 for Windows cluster. 
It has every HDP service component installed, all on the single node's host
name. It is using Derby for the metastore database.

The cluster properties used for this single node cluster:

    #Log directory
    HDP_LOG_DIR=c:\hadoop\logs

    #Data directory
    HDP_DATA_DIR=c:\hdpdata

    #hosts
    NAMENODE_HOST=WIN-NJT8GP7961S
    SECONDARY_NAMENODE_HOST=WIN-NJT8GP7961S
    RESOURCEMANAGER_HOST=WIN-NJT8GP7961S
    HIVE_SERVER_HOST=WIN-NJT8GP7961S
    OOZIE_SERVER_HOST=WIN-NJT8GP7961S
    WEBHCAT_HOST=WIN-NJT8GP7961S
    SLAVE_HOSTS=WIN-NJT8GP7961S
    CLIENT_HOSTS=WIN-NJT8GP7961S
    HBASE_MASTER=WIN-NJT8GP7961S
    HBASE_REGIONSERVERS=WIN-NJT8GP7961S
    ZOOKEEPER_HOSTS=WIN-NJT8GP7961S
    FLUME_HOSTS=WIN-NJT8GP7961S

    #Database host
    DB_FLAVOR=DERBY
    DB_HOSTNAME=WIN-NJT8GP7961S
    DB_PORT=1527

    #Hive properties
    HIVE_DB_NAME=hive
    HIVE_DB_USERNAME=hive
    HIVE_DB_PASSWORD=hive

    #Oozie properties
    OOZIE_DB_NAME=oozie
    OOZIE_DB_USERNAME=oozie
    OOZIE_DB_PASSWORD=oozie
  
