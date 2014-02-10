# Guide: Scripting Pre-requisite deploy and setup

### Configuring Java

Once Java is installed, create a JAVA_HOME system environment variable:

    setx JAVA_HOME "C:\java\jdk1.6.0_31" /m


### Configuring Python

Once Python is installed, add the executable to the PATH system environment 
variable:

    setx PATH "$env:path;C:\Python27" /m

### References

HDP 2.0 for Windows Manual Install docs:
http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0-Win/bk_installing_hdp_for_windows/content/win-getting-ready.html    
