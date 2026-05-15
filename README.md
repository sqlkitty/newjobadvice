# New Job Week by Week 
## Menu

- [Week 1 - What Tools Do You Need?](#week-1---what-tools-do-you-need)
- [Week 2 - Creating a Checklist](#week-2---creating-a-checklist)
  - [Checklist of Items to Analyze](#checklist-of-items-to-analyze)
  - [Highest and Lowest Priority Items](#highest-and-lowest-priority-items)
  - [Skills Required?](#skills-required)
- [Week 3 - Creating Alerts](#week-3---creating-alerts)
  - [Get Started](#get-started)
  - [Terraform Components](#terraform-components)
  - [Creating Resources](#creating-resources)
  - [Creating Azure SQL Database](#creating-azure-sql-database)
- [Week 4 - Setup Auditing](#week-4---setup-auditing)
  - [Configure Auditing](#configure-auditing)
  - [Querying Audit Data](#querying-audit-data)
  - [Reporting on Audit Data](#reporting-on-audit-data)

## Week 1 - What Tools Do You Need?

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

## Week 2 - Creating a Checklist

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

## Week 3 - Creating Alerts 


**UPDATED**: I needed to change out resources that will be deprecated, such as azurerm\_mssql\_database, azurerm\_mssql\_firewall\_rule, and azurerm\_mssql\_server. Code snippets in this post and GitHub are updated accordingly.

**The main goal for week 3: set up much-needed alerts on DTU percentage and disk space percentage for all Azure SQL Databases.** This week is about learning Terraform or at least some Terraform. Enough Terraform to create a test Azure SQL database and put alerts on it. I decided that my first task here is to get alerting set up properly. I’m using Terraform because my company requires this for infrastructure management. I’m setting up a home lab because I don’t want to practice my entry-level Terraform skills on work resources.

Can you set up an Azure SQL database and alerting without all this automation? Yes, you can. This post isn’t about that because you can find a [tutorial](https://learn.microsoft.com/en-us/azure/azure-sql/database/alerts-insights-configure-portal?view=azuresql) to walk you through all that via the Azure portal. This also isn’t a detailed tutorial on how you can use all these tools.

Here are some good resources for learning more about Terraform:

-   If you have LinkedIn Learning, this is a [very helpful course](https://www.linkedin.com/learning/introduction-to-terraform-on-azure/getting-started?autoplay=true) by Alexandra Illarionov.
-   If you want to go the free route, you can get help directly from Terraform’s [tutorials](https://developer.hashicorp.com/terraform/tutorials/azure-get-started).

**TL;DR** If you want the code without much explanation, visit my [GitHub code repository](https://github.com/sqlkitty/terraform).

-   [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.3)
    
-   [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
    
-   [Terraform](https://developer.hashicorp.com/terraform/downloads) 
    
-   [GitHub Desktop](https://desktop.github.com/) or [git](https://git-scm.com/downloads) if you like the command line better – if you want to check your code into GitHub
    
-   [VS Code](https://code.visualstudio.com/download)
    
-   VSCode Terraform extension – Syntax highlighting and autocompletion for Terraform
-   [Azure account](https://portal.azure.com/#home) 
    

### Get Started

I did it like this. Is it the right way? Maybe. I’m giving you my steps so you know how this process could work.

-   On GitHub.com, create a repository for Terraform
-   Clone this repository with GitHub Desktop to a folder on your local machine
-   Open that folder in VSCode
-   Open the Terminal by clicking the Terminal menu item then choose New Terminal
-   az login – this will log you into your Azure account so that you can create resources with Terraform 

### Terraform Components

Now you can create a few files to support your Terraform process:

-   main.tf – This holds the code for the resources you will create. In my case, I put the resource group and server, and db setup in this file.
-   output.tf – This holds anything you want to output to the terminal after Terraform runs.
-   providers.tf – This holds whatever providers Terraform needs to run.
-   variables.tf – This holds variables you can use in main.tf.
-   alerts.tf – This holds the code for creating the alerts. I didn’t want my main.tf getting really long, so I split these out.

Let’s look at what each of these files will contain starting with providers.tf. Terraform will error if you don’t provide it with what providers it should use. Thank you, Microsoft, for [this helpful tutorial](https://learn.microsoft.com/en-us/azure/developer/terraform/create-resource-group?tabs=azure-cli#implement-the-terraform-code%20https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/pet). Also, a lot of helpful examples in the Terraform GitHub repository [here](https://github.com/hashicorp/terraform-provider-azurerm/tree/main/examples/sql-azure). In this case, I will use these providers:

```
terraform {
  required_version = "&gt;=0.12"

  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~&gt;2.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "~&gt;3.0"
    }
  }
}

provider "azurerm" {
  features {}
}t
```

Next up is output.tf. You don’t have to output anything. I chose to output the resource group name, SQL Server fully qualified domain name, and database name.

```
output "resource_group_name" {
  value = azurerm_resource_group.rg.name
}

output "sql_server_fqdn" {
  value = azurerm_mssql_server.example.fully_qualified_domain_name
}

output "database_name" {
  value = azurerm_mssql_database.example.name
} 
```

Next, we have variables.tf. I’ve stored a couple of variables here.

```
variable "resource_group_location" {
  default     = "eastus2"
  description = "Location of the resource group."
}

variable "resource_group_name_prefix" {
  default     = "rg"
  description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription."
}
```

Then we get to main.tf, which holds all the resources I want to create. Let’s step through this one a bit to see what we have. To begin with, I want to create a resource group to hold all my resources. I’ve also used [random\_pet](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/pet) so I always get a unique name. This way I could share the code with you, and you can run it without issue.

### Creating Resources

The following code will create a resource group with the naming convention rg-hopeful-monkey. In my case, it’s a very fitting description of me this week.

```
resource "random_pet" "rg_name" {
  prefix = var.resource_group_name_prefix
}

resource "azurerm_resource_group" "rg" {
  location = var.resource_group_location
  name     = random_pet.rg_name.id
}
```

At this point, with all my files and a resource group creation in place, I wanted to test Terraform. **Before you start, you must run terraform init at the terminal in VSCode. You can’t create any resources until after you run this init command.** Once the init is complete, you will see a terraform.tfstate file in your folder.

**Next, you can run terraform plan.** This will show you if you have any errors and let you know what it will add, change, or destroy. i.e. Plan: 1 to add, 0 to change, 0 to destroy. I’m always careful to analyze the details and especially careful with change and destroy.

If the plan looks good, you can move on to terraform apply. It will run through a plan and let you know what it plans to add, change, or destroy. **In fact, you don’t have to run a plan before apply because apply includes plan.** The apply option then asks you: Do you want to perform these actions? Enter yes to apply.

It outputs the process and what it’s working on. Then, hopefully, because you’ve done everything correctly, it says: Apply complete! Resources: 1 added, 0 changed, 0 destroyed. It will also output anything you’ve specified in the output.tf file. So in my case, it added one resource group named rg-hopeful-monkey.

### Creating Azure SQL Database

Once we have the resource group, we can add a SQL Server to it. I included the depends\_on because I want to ensure Terraform doesn’t try to create the server until the resource group is set up.

```
resource "azurerm_mssql_server" "example" {
  name                         = "sql-${azurerm_resource_group.rg.name}"
  resource_group_name          = random_pet.rg_name.id
  location                     = var.resource_group_location
  version                      = "12.0"
  administrator_login          = "sqladmin"
  administrator_login_password = "password@123!"
  depends_on = [
    azurerm_resource_group.rg
  ]
} 
```

Then we can add a SQL database to the server. I included the depends\_on because I want to ensure Terraform doesn’t try to create the database until the server is set up.

```
resource "azurerm_mssql_database" "example" {
  name                             = "db-${azurerm_resource_group.rg.name}"
  server_id                        = azurerm_mssql_server.example.id
  create_mode                      = "Default"
  sku_name                         = "Basic"
  collation                        = "SQL_Latin1_General_CP1_CI_AS"
  depends_on = [
     azurerm_mssql_server.example
   ]
}
```

To be able to log into the DB server from SSMS or Azure Data Studio, you will need firewall rules. [Get your IP](https://whatismyipaddress.com/) and change the 0.0.0.0 to your IP address.

```
resource "azurerm_mssql_firewall_rule" "example" {
  name                = "my-ip"
  server_id         = azurerm_mssql_server.example.id
  start_ip_address    = "67.164.173.44"
  end_ip_address      = "67.164.173.44"
  depends_on = [
     azurerm_mssql_database.example
   ]
} 
```

Now that you have your database in place, you can add alerts to it. First, you will need an action group, so the alerts get sent to you. I chose email alerts, but there are other options.

```
resource "azurerm_monitor_action_group" "ag" {
  name                = "dbactiongroup"
  resource_group_name = random_pet.rg_name.id
  short_name          = "dbactgrp"

  email_receiver {
    name                    = "sendtome"
    email_address           = "email@email.com"
    use_common_alert_schema = true
  }
  depends_on = [
     azurerm_mssql_database.example
   ]
}
```

Now you can create alerts. **The alerts I’m most interested in seeing are the DTU percentage and disk usage percentage. I created two alerts for each. One for a warning at 80% and one for critical at 95%.** I want to know before it becomes a huge problem. If for some reason I miss that warning, I get another alert when it is critical. I’ve included only one alert setup below. To see the rest, visit [my GitHub repository](https://github.com/sqlkitty/terraform). I included the depends\_on because I want to ensure Terraform doesn’t try to create these alerts until the database is set up.

```
resource "azurerm_monitor_metric_alert" "alertdtu80" {
  name                = "db-DTUalertMax80"
  resource_group_name = random_pet.rg_name.id
  scopes              = ["/subscriptions/4290e3cb-9352-4732-b94f-4d976370691c"]
  description         = "db DTU alert greater than 80%"
  target_resource_type = "Microsoft.Sql/servers/databases"
  target_resource_location = var.resource_group_location
  severity            = 2
  
  criteria { 
    metric_namespace = "Microsoft.Sql/servers/databases"
    metric_name      = "dtu_consumption_percent"
    aggregation      = "Maximum"
    operator         = "GreaterThan"
    threshold        = 80
  }

  action {
    action_group_id = azurerm_monitor_action_group.ag.id
  }
  depends_on = [
     azurerm_mssql_database.example
   ]
}
```

Once I’m done creating all these Terraform resources in files, I run terraform apply in the terminal. Then, once I’m happy with the tf files and they’ve all applied correctly, I will use either VS Code or GitHub Desktop to commit and push them to GitHub.

Now I will receive an email if this threshold is crossed. Hopefully, no more someone telling me there’s a problem before I know there is a problem. I may add more alerts, but for now, these basic ones will cover many of the issues that may come up in Azure SQL Database.

## Week 4 - Setup Auditing

**The main goal for week 4: set up auditing for all Azure SQL Databases.** This week is again about learning more Terraform. I’m using Terraform because my company requires this for infrastructure management. I’m setting up a home lab because I don’t want to practice my entry-level Terraform skills on work resources.

Can you set up an Azure SQL database and auditing without all this automation? Yes, you can. This post isn’t about that. I have a tutorial showing you how to manually set up auditing. Here’s the [shorter version](https://www.youtube.com/watch?v=qKvZkg_rPuM&t=1s) and the [longer version](https://www.youtube.com/watch?v=3u1sK9kgmuE&t=24s). This also isn’t a detailed tutorial on how you can use all these tools.

Here are some helpful resources for learning more about Terraform:

-   If you have LinkedIn Learning, this is a [very helpful course](https://www.linkedin.com/learning/introduction-to-terraform-on-azure/getting-started?autoplay=true) by Alexandra Illarionov.
-   If you want to go the free route, you can get help directly from Terraform’s [tutorials](https://developer.hashicorp.com/terraform/tutorials/azure-get-started).

**TL;DR** If you want the code without much explanation, visit my [GitHub code repository](https://github.com/sqlkitty/terraform).


Now that you have your Azure SQL Server in place (if you followed week 3), you can add auditing to it. First, you will need a Log Analytics Workspace to store audit data in it. I chose Log Analytics, but you can also choose Storage or Event Hub. I love Log Analytics because it’s easy to query data with Kusto. Plus, you can centralize all your database audit data in one workspace per subscription.

```
resource "azurerm_log_analytics_workspace" "example" {
  name                = "law-${azurerm_resource_group.rg.name}"
  location            = var.resource_group_location
  resource_group_name = random_pet.rg_name.id
  sku                 = "PerGB2018"
  retention_in_days   = 30
}
```

Now you can set up auditing. This means it will audit all Azure SQL databases on the server in the same way. It will put that audit data in the Log Analytics Workspace.

```
resource "azurerm_monitor_diagnostic_setting" "example" {
  name                       = "ds-${azurerm_resource_group.rg.name}"
  target_resource_id         = "${azurerm_mssql_server.example.id}/databases/master"
  log_analytics_workspace_id = azurerm_log_analytics_workspace.example.id

  enabled_log {
    category = "SQLSecurityAuditEvents"
    # enabled  = true

    retention_policy {
      enabled = false
    }
  }

  metric {
    category = "AllMetrics"

    retention_policy {
      enabled = false
    }
  }

  lifecycle {
    ignore_changes = [log, metric]
  }
}

resource "azurerm_mssql_database_extended_auditing_policy" "example" {
  database_id            = "${azurerm_mssql_server.example.id}/databases/master"
  log_monitoring_enabled = true
}

resource "azurerm_mssql_server_extended_auditing_policy" "example" {
  server_id              = azurerm_mssql_server.example.id
  log_monitoring_enabled = true
}
```

  
Once I’m done creating all these Terraform resources in files, I run terraform apply in the terminal. Then, once I’m happy with the tf files and they’ve all applied correctly, I will use either VS Code or GitHub Desktop to commit and push them to GitHub.

### Configure Auditing

There is something important to know about Azure SQL auditing. It collects everything happening in the database by default with these audit action groups:

BATCH\_COMPLETED\_GROUP

SUCCESSFUL\_DATABASE\_AUTHENTICATION\_GROUP

FAILED\_DATABASE\_AUTHENTICATION\_GROUP

For now, I’m leaving my audit action groups as default because I want to see all the queries hitting the databases. This way I can analyze them for performance tweaks that may be required. To make these changes, you will need PowerShell. I usually run this in the Azure CLI but am working out how to set this up in Terraform.

You can get your current audit action groups by executing this code:

```powershell
Get-AzSqlServerAudit -ResourceGroupName 'rg-hopeful-monkey' -Servername 'sql-rg-hopeful-monkey'
```

You can set your audit action groups to only collect schema and security changes with this code:

```powershell
Set-AzSqlServerAudit -ResourceGroupName 'rg-hopeful-monkey' -ServerName ‘sql-rg-hopeful-monkey' ` -AuditActionGroup APPLICATION_ROLE_CHANGE_PASSWORD_GROUP, DATABASE_CHANGE_GROUP, ` DATABASE_OBJECT_CHANGE_GROUP, DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP, ` DATABASE_OBJECT_PERMISSION_CHANGE_GROUP, ` DATABASE_OWNERSHIP_CHANGE_GROUP, ` DATABASE_PERMISSION_CHANGE_GROUP, DATABASE_PRINCIPAL_CHANGE_GROUP, ` DATABASE_PRINCIPAL_IMPERSONATION_GROUP, ` DATABASE_ROLE_MEMBER_CHANGE_GROUP, ` SCHEMA_OBJECT_CHANGE_GROUP, SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP, ` SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP, USER_CHANGE_PASSWORD_GROUP
```

For now, I’m leaving my audit action groups as the default because I want to see all the queries hitting the databases so I can analyze them for performance tweaks that may be required. It will also help determine unused objects. I will update this post as I figure out how to use Terraform to set these audit action groups.

### Querying Audit Data

[Here’s](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tutorials/learn-common-operators) a helpful Kusto tutorial. Kusto is very powerful and easy to use. If you know SQL, you can use Kusto easily in Log Analytics. 


```
AzureDiagnostics
| summarize QueryCountByDB = count() by database_name_s
```

Or maybe you want more details about what happened in the last day, and you can use this query:

```
AzureDiagnostics
| where Category == 'SQLSecurityAuditEvents'
   and TimeGenerated &gt; ago(1d) 
| project
    event_time_t,

    action_name_s,
    database_name_s,
    statement_s,
    server_principal_name_s,
    succeeded_s,
    client_ip_s,
    application_name_s,
    additional_information_s,
    data_sensitivity_information_s
| order by event_time_t desc
```


### Reporting on Audit Data

In the past, I used a Logic App, but that’s harder to set up with Terraform. I’m planning to create an Azure Function to do this instead. [This presentation](https://github.com/sqlkitty/conferencepresenatations/blob/main/azuresqlaudit/HandleAzureSQLAuditingWithEase_passsummit.pdf) gives you the steps I used in my logic app starting on slide 30. I will add more info on the Terraform setup of an Azure Function in a future post.
