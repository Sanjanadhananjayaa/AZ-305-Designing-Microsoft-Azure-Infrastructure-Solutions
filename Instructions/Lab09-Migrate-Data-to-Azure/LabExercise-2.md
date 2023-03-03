# Instructions

## Exercise 2: Migrate SQL Server database to Azure

In this exercise you are going to migrate SQL server database to Azure by using Data Migration Assistant.

In this exercise, you will:

+ Task 1: Create an Azure SQL database
+ Task 2: Set up server-level firewall rules using Azure Portal
+ Task 3: Install the Data Migration Assistant (DMA) on Windows
+ Task 4: Use the Data Migration Assistant to prepare for migration from SQL Server to Azure SQL Database
+ Task 5: Use Data Migration Assistant to migrate Schema and Data

### Estimated Timing: 100 minutes

### Task 1: Create an Azure SQL database

In this task, you will learn how to create an Azure SQL database by using Azure portal.

#### Steps:

1. In the home page of Azure portal, please enter **SQL database** on the search bar and select **SQL databases** from the list.

2. On the SQL databases page, please select **+ Create**.

   ![img](../media/datas1.png)

3. On the **Create SQL Database**, enter the following details.

    | Settings | Values |
    |  -- | -- |
    | Subscription | **Use default supplied** |
    | Resource group | **ODL-AZ-305M05D-XXXXX-AZ-305M05D** |
    | Database name | **contosodb1** |

    ![img](../media/datas2.png)

4. For server, click **Create new**.

5. On **Create SQL Database Server** page, enter the following details, then click **Ok**.

    | Settings | Values |
    |  -- | -- |      
    | Server name | **contososerv(Deplyoment-id)** |
    | Location | **East US** |
    | Authentication method | **Use SQL authentication** |
    | Server admin login | **contosoadmin** 
    | Password |  **Contoso@123** 
    | Confirm password | **Contoso@123** |   
    
>**Note:** You can find Deployment-id from Environment Details tab. 
 
   ![img](../media/AZ-305-M9-1-0.png)

6. After creating the database server, enter the following details, then select **Review + create**. 

    | Settings | Values |
    |  -- | -- |      
    | Want to use SQL elastic pool? | **No** |    |
    | Compute + storage | **General Purpose (Standard-series (Gen5), 2 vCores, 32 GB storage, zone redundant disabled)** |
    | Backup storage redundancy |  **Locally-redundant backup storage** |

    ![img](../media/AZ-305-M9-0-02.png)

7. After the validation is passed, select **Create**.

>**Note:** The deployment will take few minutes to complete. Please wait till it succeeded. 

### Task 2: Set up server-level firewall rules using Azure Portal

In this task you will configure Server firewall. Azure SQL Server is protected by server-level firewall rules. As a result, it applies to all underlying Azure SQL Databases. Before reaching the Azure server or database, each connection must pass through the firewall.

#### Steps:

1. In the Azure portal, go to the database you have created in the previous task. Select **Set Server Firewall** on the **Overview** section.

   ![img](../media/AZ-305-M9-02.png)

2. On the Networking page, select **Selected Networks**. To add your current IP address to a new server-level firewall rule, select **+ Add your client IPv4 address**. This rule has the ability to open Port 1433 for a single IP address or a range of IP addresses, then select **Save**.

   ![img](../media/datas6.png)

3. Go to **contosodb1** database, select **Query editor (Preview)** provide the login as **contosoadmin** and Password **Contoso@123** then click on **Ok**.

You have successfully logged into the contosodb1 database.

### Task 3: Install the Data Migration Assistant (DMA) on Windows

In this task, you will learn how to install and configure Data Migration Assistant (DMA) on Windows.

#### Steps:
 
1. Open up your web browser, and go to the download page for Microsoft Data Migration Assistant, please click [here](https://www.microsoft.com/en-us/download/details.aspx?id=53595).
    
    >**Note:** Please follow the steps in this task even if DMA is already installed, to ensure that you are using the latest version of the tool.

2. Confirm that your environment supports the software by checking the requirements list. If it asks for installing .Net Framework 4.8 please click [here](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net48) to download. After downloading it, please go to the **Downloads** folder in **File explorer** and double click on the .Net installer file named **ndp48-web** to install it.

3. To download **DataMigrationAssistant.msi**, double click on the installer file in **Downloads** folder, and then select **Run**.

4. On the **Welcome** screen, select **Next**.

5. Select **I accept the terms in the License Agreement**, and then click on **Next**.

6. Read the **Privacy Statement**, and then select **Install**.

7. If prompted, allow UAC control for this application.

8. To complete install, select **Finish**.

### Task 4: Use the Data Migration Assistant to prepare for migration from SQL Server to Azure SQL Database

#### Steps:

1. Select the **Start** button, type **Data Migration**, and then select **Microsoft Data Migration Assistant**.

2. To create a new project, on the left, select **+**.

    ![img](../media/datam1.png)

3. On the **New** page, enter these values, and then select **Create**:

    | Property | Value |
    | --- | --- |
    | Project type | **Assessment** |
    | Project name | **Migration Assessment SQL DB** |
    | Assessment type | Database Engine |
    | Source server type | SQL Server |
    | Target server type | Azure SQL Database |
    
    
    ![img](../media/datam2.png)  

4. On the **Options** page, leave the default values, and then select **Next**.

5. On the **Connect to a server** page, enter these values, and then select **Connect**:

    | Property | Value |
    | --- | --- |
    | Server name | **labvm-XXXXXX\SQLEXPRESS** (Please go to SSMS and take the server name from there). |
    | Authentication type | **Windows Authentication** |
    | Encrypt connection | Deselected |
    | Trust server certificate | Selected |

    ![img](../media/datam3a.png) 

6. On the **Add sources** page, select the **AdventureWorks** database, and click on **Add**.

    ![img](../media/datam4.png) 

7. On the **Select sources** page, select **Start Assessment**.

8. Review the SQL Server feature parity and compatibility issues found. Note how many feature parity issue have been found.

    ![img](../media/datam5.png) 

9. Go to SSMS, right click on the server name, then select **Properties**.

    ![img](../media/datam6.png)

10. On the **Server properties** window, select **Security**, then select **SQL Server and Windows Authentication** mode and click on **Ok**. 

    ![img](../media/datam7.png)

11. In Azure portal, go to **contosodb1** database, then select **Query editor**.

12. Login with username as **contosoadmin** and Password as **Contoso@123**.

13. Expand the **Tables**, you can see there are no tables listed.

### Task 5: Use Data Migration Assistant to migrate Schema and Data

#### Steps:

1. Open the **Microsoft Data Migration Assistant** tool, select the **+** New (+) icon. Enter the following details and then select **Create**.

    | Property | Value |
    | --- | --- |
    | Project type | **Migration** |
    | Project name | **contosodatamigration** |
    | Source server type | Select **SQL Server** |
    | Target server type | Select **Azure SQL Database** |
    | Migration scope | Select **Schema and Data** |

    ![img](../media/datam8.png)

2. On the Select Source tab, select the server name **labvm-XXXXX\SQLEXPRESS**, then select **Windows Authentication** as Authentication type, and click on **Connect**. 

    ![img](../media/datam9.png)

3. Select **Adventureworks2019**, then select **Next**.

4. Go to **contosodb1** database on azure portal, on the **Overview** section, copy the server name **contososervxxxxxx.database.windows.net**.

5. Go to **Microsoft Data Migration Assistant** tool and on the **Connect to target server** tab on the server name section, paste the contosdb1 server name copied.

6. For the **Authentication type** please select **SQL Server Authentication**, then enter username as **contosoadmin**, and password as **Contoso@123**.

7. For the **Connection properties** please deselect **Encrypt connection** and select **Trust server certificate**.

8. Select **Connect**.

     ![img](../media/datam10.png)

9. Select **contosodb1** and then click on **Next**

10. On the **Select Objects** tab, select the **Schema** (By default all the objects are selected, please deselect all other objects except schema).

11. To create the SQL scripts, select **Generate SQL scripts option**.

    ![img](../media/datam11.png)

12. On the **Script & Deploy schema** tab, select **Deploy schema**.

    ![img](../media/datam12.png)

13. You have successfully migrated the schema, you can see the execution of all the schema queries are successfully completed.

    ![img](../media/datam13.png)


14. Go to Azure portal and select the database named **contosodb1**.  Go to the **Query Editor** and paste the below T-SQL script, then click on **Run** to create a table named **HumanResources.EmployeeDepartmentHistory**.

    ```T-SQL
    CREATE TABLE [HumanResources].[EmployeeDepartmentHistory](
	[BusinessEntityID] [int] NOT NULL,
	[DepartmentID] [smallint] NOT NULL,
	[ShiftID] [tinyint] NOT NULL,
	[StartDate] [date] NOT NULL,
	[EndDate] [date] NULL,
	[ModifiedDate] [datetime] NOT NULL,
    CONSTRAINT [PK_EmployeeDepartmentHistory_BusinessEntityID_StartDate_DepartmentID] PRIMARY KEY CLUSTERED 
    (
	[BusinessEntityID] ASC,
	[StartDate] ASC,
	[DepartmentID] ASC,
	[ShiftID] ASC
    )WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON         [PRIMARY]
    ) ON [PRIMARY]
    GO
    ```

    ![img](../media/AZ-305-M9-3.png)

15. You have successfully created the table named **HumanResources.EmployeeDepartmentHistory**. Expand the Tables and you can see the newly created table.

    ![img](../media/AZ-305-M9-4.png)


You are going to migrate from on-premises database Adventureworks2019 table named **HumanResources.EmployeeDepartmentHistory** data to Azure SQL database named **contosodb1** and the  table named **HumanResources.EmployeeDepartmentHistory**.

16. Go to **Microsoft Data Migration Assistant** tool, then click on **Migrate data**.

    ![img](../media/datab3.png)

17. On the **Select tables** tab, select **HumanResources.EmployeeDepartmentHistory** table, then select **Start data migration**. 

    ![img](../media/datab4.png)

18. Once the migration is completed, you will get a successfull message on **Migrate data** tab.

    ![img](../media/datab5.png)

19. Go to Azure portal, open **contosodb1** database and select **Query editor**, enter username and password.

20. Right click on **HumanResources.EmployeeDepartmentHistory** table and select **Select top 1000 rows**. You can see the data retrieved on the result pane.

    ![img](../media/AZ-305-M9-05.png)

You have successfully migrated the data.

#### Review

In this exercise, you have:

- Created an Azure SQL database
- Configured server-level firewall rules using Azure Portal
- Installed the Data Migration Assistant (DMA) on Windows
- Used the Data Migration Assistant to prepare for migration from SQL Server to Azure SQL Database
- Used Data Migration Assistant to migrate Schema and Data

