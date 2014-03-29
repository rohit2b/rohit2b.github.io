# Troubleshooting Help

This guide will outline some of the common installation failures, how to detect and then how to fix them.

### HDP FAILURE: Failed to create Hadoop user

Detection: In the install log file, you will see:

    CREATE-USER FAILURE: Exception calling "SetInfo"  with "0"
    ...
    argument(s): "The password does not meet the password policy requirements. 
    Check the minimum password length, password complexity and password history 
    requirements."
    ...
    Write-Log : HDP FAILURE: Failed to create Hadoop user
    ...
    Error 0x80070001: Command line returned an error.
    ...
    Error 0x80070001: CAQuietExec Failed

Root cause: The password you specified for 'hadoop' user does not meet the Windows machine password policy requirements.

Solution: Re-run installer and use a password that meets the policy requirements.
ToDo: Add where to find the Windows policy
