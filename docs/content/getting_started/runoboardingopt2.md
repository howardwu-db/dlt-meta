---
title: "Run Onboarding"
date: 2021-08-04T14:25:26-04:00
weight: 18
draft: false
---

#### Option#2: Python whl job
1. Go to your Databricks landing page and do one of the following:

2. In the sidebar, click Jobs Icon Workflows and click Create Job Button.

3. In the sidebar, click New Icon New and select Job from the menu.

4. In the task dialog box that appears on the Tasks tab, replace Add a name for your job… with your job name, for example, Python wheel example.

5. In Task name, enter a name for the task, for example, ```dlt_meta_onboarding_pythonwheel_task```.

6. In Type, select Python wheel.

7. In Package name, enter ```dlt_meta```.

8. In Entry point, enter ``run``. 

9. Click Add under Dependent Libraries. In the Add dependent library dialog, under Library Type, click PyPI. Enter Package = ```dlt-meta```

10. Click Add.

11. In Parameters, select keyword argument then select JSON. Past below json parameters with :
- Without Unity Cataglog
```json 
    {                   
        "onboard_layer": "bronze_silver",
        "database": "dlt_demo",
        "onboarding_file_path": "dbfs:/onboarding_files/users_onboarding.json",
        "silver_dataflowspec_table": "silver_dataflowspec_table",
        "silver_dataflowspec_path": "dbfs:/onboarding_tables_cdc/silver",
        "bronze_dataflowspec_table": "bronze_dataflowspec_table",
        "import_author": "Ravi",
        "version": "v1",
        "bronze_dataflowspec_path": "dbfs:/onboarding_tables_cdc/bronze",
        "onboard_layer": "bronze_silver",
        "uc_enabled": "False",
        "overwrite": "True",
        "env": "dev"
    } 
```
- with Unity catalog
```json 
    {                   
        "onboard_layer": "bronze_silver",
        "database": "uc_name.dlt_demo",
        "onboarding_file_path": "dbfs:/onboarding_files/users_onboarding.json",
        "silver_dataflowspec_table": "silver_dataflowspec_table",
        "bronze_dataflowspec_table": "bronze_dataflowspec_table",
        "import_author": "Ravi",
        "version": "v1",
        "onboard_layer": "bronze_silver",
        "uc_enabled": "True",
        "overwrite": "True",
        "env": "dev"
    } 
```
- Note in database field you need to provide catalog name then schema name as `<<uc_name>>.<<schema>> `

Alternatly you can enter keyword arguments, click + Add and enter a key and value. Click + Add again to enter more arguments. 

12. Click Save task.

13. Run now

14. Make sure job run successfully. Verify metadata in your dataflow spec tables entered in step: 11 e.g ```dlt_demo.bronze_dataflowspec_table``` , ```dlt_demo.silver_dataflowspec_table```
