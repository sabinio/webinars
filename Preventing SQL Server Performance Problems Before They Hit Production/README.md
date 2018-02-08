# SentryOne Deployment Pipeline Demo

- Download WideWorldImporters demo database (WideWorldImporters-Full.bak) from: https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0

- Using SQL Server Management Studio (SSMS), Restore the database download to SQL Server 2016 or Later.

  - (The AdventureWorks database could be restored on older versions of SQL Server. This will require Modifying the deployment condition)

## From the [SentryOne Repository](https://github.com/sabinio/SentryOne)

- Open the __[DeploymentSchedule.sql](https://github.com/sabinio/SentryOne/tree/master/Conditions/SabinIO%20Deployment.condition/DeploymentSchedule.sql)__ in SSMS and change the USE statement to point to the correct database.
- Execute the DeploymentSchedule.sql script.
- Monitor the SQL Server instance with SentryOne.
- In SentryOne open Advisory Conditions list from Navigator.
- Right click any current Condition and click Import, Select each __[SabinIO Condition](https://github.com/sabinio/SentryOne/tree/master/Conditions/)__ to import.
  - If a Different database than WideWorldImporters is used, right click the SabinIO Deployment Advisory Condition in SentryOne and select Edit. Change the Database Name from WideWorldImporters to the desired database name.
- Test SabinIO Deployment Advisory Condition by inserting a record into the DeploymentSchedule table using the sp_DeploymentSchedule_i stored procedure, then execute the sp_DeploymentSchedule_u with the same ReleaseName to enter and end time for the release.
  - EXEC sp_DeploymentSchedule_i @ReleaseDefinitionName = 'TestDefinition', @ReleaseName = 'TestRelease', @ReleaseDescription = 'Code Change', @ReleaseEnv = 'PreProd'
  - EXEC sp_DeploymentSchedule_u @ReleaseName = 'TestRelease'
- Check the SentryOne Performance Advisor dashboard for any Alerts.