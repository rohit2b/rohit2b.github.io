# Setting up a user in HDP 2.0 for Windows

Hadoop provides authorization mechanisms that protects access to datasets. This ensures that only authorized users and applications are allowed to write and read data in Hadoop.
These authorizations need to be enabled for each user and group.

In this guide, we will walk through the steps to enable a Windows user to:
- Write and read data to HDFS
- Execute applications that have permissions to write and read data to HDFS

### The setup

For this guide, I have set up a one node HDP 2.0 for Windows cluster. This cluster has the following components installed on the node:

- Hadoop Core (HDFS and YARN)
- Hive
- Pig
- Oozie
- Sqoop
- Mahout


This is a screenshot of my installed services on the node:

<image here>

This is a screenshot of the installed directories as part of the HDP install

<image here> 

### Windows user

I am logged into the Windows node as user 'root'. This is an administrator account, and I want to use this user to write/read/run jobs on my Hadoop single node cluster.

Tip: To view all local users on the node, run this in Powershell:

    > net users

Tip: To find out what user you are currently logged in as, run this in Powershell:

    > whoami

### Switching to Hadoop Admin user

Log into the HDP admin account. This is 'hadoop'. 

    > runas /user:hadoop /savecred cmd

This will prompt for the 'hadoop' user password. Upon entering that, you will be taken to a new CMD window logged in as 'hadoop'.

### Setting permissions for HDFS directories

Ensure that the MapReduce directory is accessible to all users. By default, after a fresh install, the /mapred directory permissions are set to 770:

    > hadoop fs -ls /
    drwxrwx---   - hadoop hdfs          0 2014-03-21 13:47 /mapred

Make this 757:

    > hadoop fs -chmod -R 757 /mapred

Create HDFS user directories for the user that you want to add. In this case, the user is 'root':

    > hadoop fs -mkdir -p /user/root

Change ownership of the HDFS directory to the 'root' user:

    > hadoop fs -chown -R root /user/root

### Validate that you have the correct permissions

Open a powershell window as user 'root'. Then try to read the directories created and modified above to validate the steps:

    > hadoop fs -ls /user
    drwxr-xr-x   - root hdfs          0 2014-03-21 14:39 /user/root

    > hadoop fs -ls /mapred
    drwxr-xrwx   - hadoop hdfs          0 2014-03-21 13:47 /mapred/history

### Validate by running the Hadoop smoke tests

The Hadoop smoke test loads a file into HDFS and then executes a simple word count MapReduce job with that file as input. This smoke test ensures that permissions are correct, and that MapReduce jobs can be executed and run.

Navigate to the HDP install directory.

    > cd C:\hdp

Run the smoke test for Hadoop only.

    > .\Run-SmokeTests.cmd hadoop

This will kick off the job. At the end, on success you will see this final message printed to console:

    Hadoop Smoke Test: PASSED

### Troubleshooting Mapreduce job failures

In case you need to troubleshoot why a MapReduce job is failing, I recommend you use the following tools and troubleshooting path:

Look at all MapReduce jobs that have been run in the ResourceManager UI, which is located at the URI: http://<Hostname>:8088

Here, find the application ID for the MapReduce job that failed and click on the URL that is the Application ID number.

Here you will see the Diagnostics info with a stack trace that represents the exception. For further troubleshooting, there are ApplicationMaster logs that are linked to at the bottom of the page. 
