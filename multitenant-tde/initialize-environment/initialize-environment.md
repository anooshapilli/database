# Initialize Environment

## Introduction

In this lab we will review and startup all components required to successfully run this workshop.

*Estimated Time:* 30 Minutes.

Watch the video below for a quick walk-through of the lab.
[Initialize Environment](videohub:1_o155nu8l)

### Objectives
- Initialize the workshop environment.

### Prerequisites
This lab assumes you have:
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- You have completed:
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup

**NOTE:** *When doing Copy/Paste using the convenient* **Copy** *function used throughout the guide, you must hit the* **ENTER** *key after pasting. Otherwise the last line will remain in the buffer until you hit* **ENTER!**

## Task 1: Validate That Required Processes are Up and Running.

1. Now with access to your remote desktop session, proceed as indicated below to validate your environment before you start executing the subsequent labs. The following Processes should be up and running:

    - Database Listeners
        - LISTENER (1521)
        - LISTCDB2 (1522)
    - Database Server Instances
        - CDB1
        - CDB2

    ![Landing page](./images/remote-desktop-landing.png " ")

2. Click the *Terminal* icon on the desktop to launch a session, then run the following to validate that expected processes are up.

    ```
    <copy>
    ps -ef|grep LIST|grep -v grep
    ps -ef|grep ora_|grep pmon|grep -v grep
    systemctl status oracle-database oracle-db-listener
    </copy>
    ```

    ![Check PMON Database process status](./images/check-pmon-up.png "check PMON Database process status")
    ![Check database service status](./images/check-db-service-up.png "Check database service status")
    ![Check DB listener service status](./images/check-dblistner-service-up.png "Check DB listener service status")

    If all expected processes are shown in your output as seen above, then your environment is ready for the next task.  

3. If you see questionable output(s), failure or down component(s), refer to the appendix section to restart the service accordingly

4. Follow the (3) steps shown below to launch *SQL Developer*:

    ![Launch SQL Developer](./images/launch-sqldeveloper.png "Launch SQL Developer")

5. Test database connectivity by clicking on the *+* sign next to each CDB or PDB listed as shown below

    ![Test Database Connections](./images/test-database-connections.png "Test Database Connections")

## Task 2: Initialize Database for Multitenant Use Cases

1. From your remote desktop session as user *oracle*, run the block below to refresh labs artifacts

    ```
    <copy>
    clear
    cd ~oracle/labs
    rm -rf ~oracle/labs/*
    wget -O novnc-multitenant.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/OsVZaMBsS-TArKa1EQNkZSB0SGptkNZwSd21lloGfE27nsRinQNvRm0G9ekds4zB/n/c4u04/b/livelabsfiles/o/labfiles/novnc-multitenant.zip
    unzip -qo novnc-multitenant.zip
    rm -f novnc-multitenant.zip
    cd multitenant
    chmod +x *.sh
    ls -ltrh
    chmod +x tde/*.sh
    ls -ltrh tde
    </copy>
    ```

    ![](./images/init-multitenant-tde.png " ")

<!-- for 21c image only. -->
2. Create Database Links. During this workshop you will use database links *`cdb1_dblink`* and *`cdb2_dblink`* to perform tasks across between the two CDBs

    ```
    <copy>
    cat initCDBs.sh
    . ./initCDBs.sh
    </copy>
    ```

You may now proceed to the next lab.

## Appendix 1: Managing Startup Services

1. Database service (All databases and Standard Listener).

    - Start

    ```
    <copy>
    sudo systemctl start oracle-database
    </copy>
    ```
    - Stop

    ```
    <copy>
    sudo systemctl stop oracle-database
    </copy>
    ```

    - Status

    ```
    <copy>
    systemctl status oracle-database
    </copy>
    ```

    - Restart

    ```
    <copy>
    sudo systemctl restart oracle-database
    </copy>
    ```

2. Database service (Non-Standard Listeners).

    - Start

    ```
    <copy>
    sudo systemctl start oracle-db-listener
    </copy>
    ```
    - Stop

    ```
    <copy>
    sudo systemctl stop oracle-db-listener
    </copy>
    ```

    - Status

    ```
    <copy>
    systemctl status oracle-db-listener
    </copy>
    ```

    - Restart

    ```
    <copy>
    sudo systemctl restart oracle-db-listener
    </copy>
    ```

## Acknowledgements
* **Author** - Rene Fontcha, LiveLabs Platform Lead, NA Technology
- **Contributors** - Sean Provost, Mike Sweeney, Bryan Grenn, Bill Pritchett
- **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, August 2023
