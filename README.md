# New Job Week by Week 

## Week 1

I changed to a new job and started it this week (March 2023). Before I started, I thought of all the things I thought I would want to do when I arrived. I don’t have a fancy, exact list of things I would do, so it’s time to make one. The thing is this is **the first time I’m working in an environment that’s entirely in the cloud**. There are no VMs so no traditional SQL Server setups. I have a long list of ideas I would do with SQL Server when I start working at a new job, but I don’t have a list for Azure. We had Azure SQL and Azure PostgreSQL at my last job. We also had Oracle, SQL Server, PostgreSQL, and their cloud varieties. There was so much other DB tech there that the Azure DBs didn’t get the love they need.

As I got to thinking about what I would do, I realized I needed a list of tools I would install. This list would enable me to work on my projects and tasks. **These tools are the same tools I used when I was managing traditional SQL Server and PostgreSQL on VMs, as well.** They work well for cloud or on-premises databases.

-   **SQL Server Management Studio** – I still use this for Azure SQL databases even though I could use Azure Data Studio. I like the feel of SSMS. Starting with version 18.7, Azure Data Studio can be installed with SSMS. [Download SSMS](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16)
-   **Azure Data Studio** – I do use this on occasion because it has schema compare functionality in it. We also have Azure PostgreSQL here so ADS comes in handy for that. [Download Azure Data Studio](https://learn.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio?view=sql-server-ver16&tabs=redhat-install%2Credhat-uninstall)
    -   [Schema Compare Extension](https://learn.microsoft.com/en-us/sql/azure-data-studio/extensions/schema-compare-extension?view=sql-server-ver16) – Make sure you are connected to each db you want to compare. I wasn’t and then wondered why it didn’t see that db.
-   **Azure Storage Explorer** – This makes is way easier to connect to and manage your storage accounts. [Download Azure Storage Explorer](https://azure.microsoft.com/en-us/products/storage/storage-explorer/)
-   **pgAdmin** – I still like this for managing Postgres databases. Even though I could use Azure Data Studio, I may fall back into pgAdmin. Plus, pgAdmin doesn’t allow all the same options for logging in as ADS. It’s harder with AD credentials with Azure PG so sometimes ADS is better. [Download pgAdmin](https://www.pgadmin.org/download/)
-   **VS Code** – This tool is versatile for file editing, and also has integration with GitHub. You can push, pull, and commit right from VS Code. [Download VS Code](https://code.visualstudio.com/download)
-   **Notepad++** – I like this for random bits of stuff I’m working on. You can configure Git to use Notepad++ as its default editor. [Download Notepad++](https://notepad-plus-plus.org/downloads/v8.5/)
-   **Git** – You will need this installed for source control integration to work in VS Code. You can then also use it from the command line if that’s your thing. You can also download it via VS Code. [Download Git](https://git-scm.com/downloads)
-   **GitHub Desktop** – If you don’t want to use Git with VS Code, this is a helpful nice interface for GitHub. [Download GitHub Desktop](https://desktop.github.com/)
-   **Docker Desktop** – This is good for running local instances of SQL Server and PostgreSQL. [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)
-   **draw.io** – I love this for diagramming. [Download draw.io](https://draw-io.en.softonic.com/)
-   **Greenshot** – This is an excellent screenshot tool and much nicer than anything built-in. [Download Greenshot](https://getgreenshot.org/downloads/)
-   **Brave** – My new favorite browser. Uses less memory and has more tracker blocking. [Download Brave](https://brave.com/)

## Week 2 

Last week was the first week of the rest of my life. But really it was the first week of my new job and I installed a lot of tools. You can learn more about those [in this blog post](https://sqlkitty.com/new-job-week-1-what-tools-do-you-need/). I also started thinking about how I would analyze existing databases. My focus is on Azure SQL right now. This post doesn’t include details about Azure PostgreSQL. I will hit those highlights in future blog posts. This post will outline the checklist I came up with in week two of my new job.

### Checklist of Items to Analyze

-   **Baselining** – Do we know what is normal and abnormal for our database servers? [Here](https://solutioncenter.apexsql.com/how-to-master-sql-server-performance-baselining-to-avoid-false-positives-and-or-missing-alerts/)‘s a helpful resource on baselining.
-   **Monitoring** – Is everything monitored properly?
-   **Alerting** – Are we getting alerts for things we need to know? Some essential ones are:
    -   DTU %
    -   Disk usage %
-   **Data retention and archiving** – Do we have partitioning in place for large tables or tables that could grow larger?
-   **Data types** – Are we using appropriate data types based on the data being stored?
-   **Indexing** – Do we have proper indexing? Are queries using the indexes properly?
-   **Index maintenance** – Do we have index maintenance scheduled and running properly?
-   **Auditing** – Do we audit to ensure we know when users make changes that could impact uptime or performance?
-   **Finding Invalid/Broken Items** – For example, what views or stored procedures reference missing objects?
-   **Perms review** – Who has access to what? And should they have this level of access?
-   **Vulnerability assessments** – Are there any settings on your database/server that put you at risk?

I only have Azure-managed databases. The list of stuff I need to know is shorter than if I used SQL Server on a VM, for example. In Azure SQL, there’s a lot less to manage because you don’t have to maintain the VM and all the server settings. On SQL Server, I would check all kinds of other stuff, like:

-   **Backups** – You don’t need agent jobs in Azure to do this like on SQL Server. You will need to decide how redundant you want the backups to be, but they will automatically take them for you. Click [here](https://learn.microsoft.com/en-us/azure/azure-sql/database/automated-backups-overview?view=azuresql) for more info.
-   **Integrity checks** – You don’t need to do this in Azure. Click [here](https://azure.microsoft.com/en-gb/blog/data-integrity-in-azure-sql-database/) for more info.
-   **Server settings** – Far fewer server settings in Azure – look this up
-   **Agent settings and jobs** – There’s no agent in Azure SQL

### Highest and Lowest Priority Items

Today’s post is about what you would look for when you arrive. **This is the point at which I would create a checklist of what I want to resolve over time.**

**For me monitoring, alerting, and auditing are at the top of the list.** We need to know when something is going or has gone wrong. **Next up, is indexing and index maintenance.** Then I would tackle more long-term projects such as poorly chosen data types and partitioning.

Your priorities may vary depending on what challenges you face. Maybe you have a VERY large table and the data needs to be deleted ASAP. In this case, you may need to partition it before you work on other items. Maybe your users are experiencing bad performance. In this case, you may need to look at indexing and queries first.

Monitoring and alerting being one of your first orders of business can’t serve you wrong, though. You need to know when the database or server is experiencing issues. This way you aren’t finding out from someone else first.

### Skills Required?

**What I realized after managing a lot of Azure databases is I need more PowerShell skills.** I need to check a bunch of settings across all these databases. I want to loop through them with PowerShell and have the results displayed cleanly for all of them at once. As it is now, I can cobble scripts together, but I want the ability to start typing and come up with a script that works.

On top of all that, **I also need to learn more Terraform.** We manage our infrastructure with Terraform. Let’s say I want to create a Log Analytics Workspace to store my audit data or create an alert for DTU. I need to use Terraform for this.

Additionally, **I need to learn Flyway and Azure DevOps** because we use them to deploy DDL code. I need to install some stored procs for baselining and they need to be put into a new schema. Flyway can manage that.

**You don’t need PowerShell, Terraform, or Flyway to accomplish this checklist. However, learning and implementing them is well worth the time it will take. It will make your life simpler in the long run by automating manual tasks.**

I’m going to use a few different things:

-   **PowerShell** – I will use this to loop through my databases to check settings. I can also use this to run scripts against multiple databases. I won’t apply settings to anything in Azure Portal with PowerShell because I will use Terraform/Flyway for that. I can also use these PowerShell modules to check settings and get recommendations for improvements:
    
    -   **dbachecks** – This PowerShell [module](https://dbachecks.readthedocs.io/en/latest/) helps you validate your environment. [Here](https://jesspomfret.com/dbachecks-and-azure-sql-databases/)‘s a helpful tutorial on how to use it.
    
    -   **dbatools** – A PowerShell [module](https://dbatools.io/) that helps you do administrative tasks. [Here](https://sqldbawithabeard.com/tag/azure-sql-database/)‘s a great tutorial on how to use it.
-   **Terraform** – I will set up infrastructure such as Log Analytics workspaces or monitoring/alerting/auditing settings for databases. Learn more about Terraform [here](https://www.terraform.io/).
-   **SQL** **with Flyway** – Naturally with SQL databases we will use SQL. I will implement the SQL on multiple Azure SQL databases with Flyway. Learn more about Flyway [here](https://flywaydb.org/).
    
    -   **Ola** – The [stored procs](https://ola.hallengren.com/sql-server-index-and-statistics-maintenance.html) I will need for index maintenance.
    -   **sp\_whoisactive** – This is a [stored proc](https://github.com/amachanic/sp_whoisactive/releases) for checking active queries.
    -   **Glenn Berry** – He has a set of [database diagnostic information queries](https://glennsqlperformance.com/resources/). There are different types of queries for SQL Server, Azure SQL, and Azure SQL MI. This can be helpful for baselining.
    -   **Ozar** – He has a set of stored procedures to capture tons of info about your SQL Server or Azure SQL database in the [SQL Server First Responder Kit](https://github.com/BrentOzarULTD/SQL-Server-First-Responder-Kit/blob/dev/README.md). This could also be helpful for baselining. It’s hit and miss whether it works on Azure SQL or not, though.
    
    -   **Partitioning** – This a fairly large topic unto itself, but [here’s](https://learn.microsoft.com/en-us/sql/relational-databases/partitions/create-partitioned-tables-and-indexes?view=sql-server-ver16) some Microsoft guidance. My plan is to partition any rapidly growing tables before they become gigantic.
    -   **Invalid/broken objects** – This [stored proc](https://www.sqlservercentral.com/articles/find-invalid-objects-in-sql-server) helps you find objects referencing other objects that are gone.
    -   **Query Store** – Using [Query Store](https://learn.microsoft.com/en-us/sql/relational-databases/performance/query-store-usage-scenarios?view=sql-server-ver16), you can also get performance baselines.
-   **Azure portal or PowerShell/Terraform**
    -   **Auditing** – I have some presentations on how to set this up in Azure SQL, but I don’t use PowerShell or Terraform in them. This will give you a clear idea of how auditing works, though. [Shorter](https://www.youtube.com/watch?v=qKvZkg_rPuM) or [longer](https://www.youtube.com/watch?v=3u1sK9kgmuE) versions are available.
    -   **Index maintenance** – This is a mishmash of SQL executed in a [runbook](https://learn.microsoft.com/en-us/azure/automation/learn/automation-tutorial-runbook-textual). I don’t have the code handy, but I use Ola stored procs and Runbooks mixed together to accomplish this feat.
    -   **Baselining** – You can use the Azure portal for [Intelligent Insights](https://learn.microsoft.com/en-us/azure/azure-sql/database/intelligent-insights-overview?view=azuresql) and [Query Performance Insights](https://learn.microsoft.com/en-us/azure/azure-sql/database/query-performance-insight-use?view=azuresql).
    -   **Vulnerability assessment** – There is a [built-in assessment](https://learn.microsoft.com/en-us/azure/defender-for-cloud/sql-azure-vulnerability-assessment-overview) in the portal that you can enable to ensure you know about vulnerabilities in your database. These can include things such as excessive permissions or excessive firewall access.

My needs may vary over time, but this is a great place to start..
