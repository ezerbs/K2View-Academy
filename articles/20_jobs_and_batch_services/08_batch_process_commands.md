# Batch Commands

The following Batch commands are available in the Fabric runtime environment:

**Instances Migration**

```BATCH LUT ('LUI*','LUI2','LUI3','LUI4') FABRIC_COMMAND="sync_instance LUT.?" with ASYNC='true';```


**Broadway Flows Execution**

```BATCH LUT fabric_command="broadway LUT.SampleFlow SampleIID=?" with async=true;```


**CDC Republish**

```BATCH LUT from fabric fabric_command="cdc_republish_instance OracleLU.?" with async=true;```


## Batch Commands Summary

<table width="900pxl">
<tbody>
<tr>
<td valign="top" width="300pxl">
<p><strong>Command Name</strong></p>
</td>
<td valign="top" width="400pxl">
<p><strong>Description</strong></p>
</td>
<td valign="top" width="300pxl">
<p><strong>Example</strong></p>
</td>
</tr>

<tr>
<td valign="top" width="500pxl">
<h5>batch &ltLUT&gt[@&ltDC&gt] FABRIC_COMMAND='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_WORKERS_PER_NODE=&ltnumber&gt]]; </h5>
</td>
<td valign="top" width="400pxl">
   
<p>
Start the Batch process and sync all LU instances:
   
- DC, specify the DC name to force the Batch process in the specified DC. This can also be defined in the Affinity parameter:  
  - AFFINITY, list of nodes and DCs to be involved in the Batch process command.
- JOB_AFFINITY, affinity for the Batch process Job.
- ASYNC, defines whether the Batch process should run in a sync or async mode. Default is False.
- GENERATE_ENTITIES_FIRST, if set to True, generate all entities before processing them.
- FABRIC_COMMAND, Fabric command executed by the Batch process which can be any command that includes a '?' that represents an Entity ID. 

The following commands must be set:
  - Migration, "sync_instance <LUT>.?"
  - Broadway flow, ...
  - CDC republish, ...
- ALLOW_MULTIPLY, when set to True, multiplies executions of the same Batch process command. Default is False.
- MAX_NODES, maximum (random) nodes participating in the Batch process.
- MAX_WORKERS_PER_NODE, enables setting a lower number of maximum workers to run on each node than the maximum number of workers defined in the config.ini file. (MAX_WORKERS_PER_NODE parameter).</p>

</td>
<td valign="top" width="300pxl">
<p>batch CUSTOMER FABRIC_COMMAND="sync_instance Customer.?" with async=’true’;

This command migrates all customers from the source systems into the Fabric CUSTOMER keyspace in the Fabric database.</p>

</td>
</tr>  

<tr>
<td valign="top" width="300pxl">

<h5>batch &ltLUT>[@&ltDC&gt].&ltIG&gt fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];</h5>
</td>
<td valign="top" width="400pxl">

<p>Batch-processes, a subset of the LUI based on the Instance Group specified by the &ltIG&gt parameter.</p>

</td>
<td valign="top" width="300pxl">
<p>batch CUSTOMER.ig10CustomersList FABRIC_COMMAND="sync_instance CUST.?" with async=’true’;
This command migrates the customers defined in the ‘ig10CustomersList’ Instance Group into the CUSTOMER keyspace in the Fabric database.</p>

</td>
</tr> 

<tr>
<td valign="top" width="300pxl">

<h5>batch &ltLUT&gt[@&ltDC&gt] from &ltdb_interface&gt using ('&ltSQL&gt') fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt' [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];</h5>

</td>
<td valign="top" width="400pxl">

<p>Batch process, a subset of the LUI based on a query to a source interface defined in the &ltdb_interface&gt parameter.</p>
<td valign="top" width="300pxl">

<p>batch CUSTOMER FROM CRM_DB USING (‘select customer_id from CUSTOMER where customer_id <= 1000’) FABRIC_COMMAND="sync_instance PATIENT.?" with async=’true’;
</p>
</td>
</tr> 

<tr>
<td valign="top" width="300pxl">

<h5>batch &ltLUT>[@&ltDC&gt] from fabric fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];</h5>

</td>
<td valign="top" width="400pxl">

<p>Batch-processes, a subset of the LUI based on existing instances in Fabric in the entity table. </p>
</td>
<td valign="top" width="300pxl">

<p>batch Customer from fabric fabric_command='sync_instance Customer.?';</p>

</td>
</tr> 


<tr>
<td valign="top" width="300pxl">

<h5>batch &ltLUT>[@&ltDC&gt].(&ltinstance 1,instance 2,...&gt) fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]]</h5>

</td>
<td valign="top" width="400pxl">

<p>Batch-processes, a subset of the LUI based on a list of instances defined in the &ltinstance 1,instance 2,...&gt parameters list.</p>
</td>
<td valign="top" width="300pxl">

<p>batch Customer.('100', '101', '102','103') FABRIC_COMMAND="sync_instance PATIENT.?" with async=’true’;</p>

</td>
</tr> 
</table>


## Batch Monitoring Commands Summary

<table width="900pxl">
<tbody>
<tr>
<td valign="top" width="300pxl">
<p><strong>Command Name</strong></p>
</td>
<td valign="top" width="400pxl">
<p><strong>Description</strong></p>
</td>
<td valign="top" width="300pxl">
<p><strong>Example</strong></p>
</td>
</tr>

<tr>
<td valign="top" width="300pxl">
<h5>batch_details '&ltbatch id&gt' [STATUS='&ltstatus&gt'] [ENTITIES='&ltentity 1,entity 2,...&gt'] [AFFINITY='&ltAffinity&gt'] [LIMIT=&ltlimit&gt] [SORT_BY_PROCESS_TIME=&lttrue/false&gt]</h5>

</td>
<td valign="top" width="400pxl">

<p>
Displays the status of instances of a given Batch process ID:
   
- STATUS, which can be either WAITING, COMPLETED, FAILED.
- ENTITIES, lists of entities separated by a comma.
- AFFINITY, DCs or nodes.
- SORT_BY_PROCESS_TIME, if True, shows only the entities with the highest process time. If set, ignore all other parameters.
- LIMIT, default limit defined in the config.ini if no limit is provided as an argument. </p>
</td>
<td valign="top" width="300pxl">
<p>batch_details 'a4587541-b12d-4329-affd-7c25516c9cde';</p>
</td>
</tr> 


<tr>
<td valign="top" width="300pxl">
<h5>batch_in_process filter='&ltfilter regex&gt'</h5>

</td>
<td valign="top" width="400pxl">

<p>Lists all running Batch processes and returns the following information: 
   <li>Node ID</li>  <li>Batch process ID</li>
    <li>Entity ID</li>
    <li>LU type</li>
    <li>Time at work (ms)</li>  
    <li>exeid</li>
    <li>command|</li>
<li>Filter, must be a regex compatible argument.</li>
</p>
</td>
<td valign="top" width="300pxl">
<p></p>
</td>
</tr> 



<tr>
<td valign="top" width="300pxl">
<h5>batch_list [STATUS='&ltstatus&gt'] [FROM_DATE='&ltfrom_date&gt' [TO_DATE='&ltto_date&gt']] [FILTER=&ltfilter criteria&gt]</h5>

</td>
<td valign="top" width="400pxl">

<p>
If there are no arguments, lists all active Batch processes together with their respective status:
   
- NEW, GENERATE_IID_LIST, IN_PROGRESS, FAILED, CANCELLED, DONE, ALL
- FROM/TO_DATE, support DATE_FORMAT/DATETIME_FORMAT according to the configuration in the config.ini.
- FILTER, filters Batch processes. The filter field must be populated by a string in a Fabric command in the Batch process. 

Note that the filter supports regex.
</p>
</td>
<td valign="top" width="300pxl">
<p>
   - batch_list STATUS='ALL'; – list the history of all batch processes.
   
   - batch_list status='ALL' FILTER='sync_instance';  list the history of all batch processes. This command returns the same results as the migrate_list STATUS = ‘ALL’; command.</p>
</td>
</tr> 



<tr>
<td valign="top" width="300pxl">
<h5>batch_retry '&ltbatch id&gt'</h5>

</td>
<td valign="top" width="400pxl">

<p>If the Batch process has not been completed, resumes a previous Batch process by reprocessing all failed or unhandled entities. Otherwise, it retries the failed entities only.
   
   If the batch process is completed before the Retry command, Fabric gets the list of instances from the source DB. 
   
   If the batch process is completed before the Retry command, Fabric gets the list of failed entities from batchprocess_entities_errors Cassandra table.
</p>
</td>
<td valign="top" width="300pxl">
<p>
batch_retry ‘161f9717-bd93-4882-a3aa-7b58c1f61b27’; 
</p>
</td>
</tr> 


<tr>
<td valign="top" width="300pxl">
<h5>cancel batch ['&ltbatch id&gt']</h5>
</td>
<td valign="top" width="400pxl">
<p>
Cancels the last started batch process coordinated by the current node. The Cancel command must be executed from the node that started the operation. 
When adding the '&ltbatch id&gt' parameter, the batch processed with the defined batch ID is cancelled whereby the Cancel command does not need to run from the node coordinating the specific batch process.

</p>
</td>
<td valign="top" width="300pxl">
<p>
Cancel batch;
</p>
Cancel batch ‘568114fe-9ec8-4c9e-af11-6e3348eff6e9’;  
</p>
</td>
</tr> 



<tr>
<td valign="top" width="300pxl">
<h5>batch_summary '&ltbatch id&gt'</h5>

</td>
<td valign="top" width="400pxl">

<p>This report brings a table holding a summary about node, DC and cluster levels.                                    
</p>
</td>
<td valign="top" width="300pxl">
<p>batch_summary '35408af6-b26a-4243-bc95-f114335bfa5e'</p>
</td>
</tr> 


<tr>
<td valign="top" width="300pxl">
<h5>batchF </h5>

</td>
<td valign="top" width="400pxl">

<p>Runs the batch process on a list of instances that are saved with a name defined within a function.</p>
<p>
1) batchf &ltLUT>[@&ltDC&gt].&ltfunction&gt() FABRIC_COMMAND='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];
</p>
<p>
2) batchf &ltLUT&gt[@&ltDC&gt].&ltfunction&gt().&ltIG&gt fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];
</p>
<p>
3) batchf &ltLUT&gt[@&ltDC&gt].&ltfunction&gt() from &ltdb_interface&gt using ('&ltSQL&gt') fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_ENTITIES_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];
</p>
<p>
4) batchf &ltLUT&gt[@&ltDC&gt].&ltfunction&gt().(&ltinstance 1,instance 2,etc...&gt) fabric_command='&ltfabric command&gt ?' [WITH [AFFINITY='&ltaffinity&gt']</p>
</td>

<td valign="top" width="300pxl">
<p>
1) batchf Customer.batchFtest4().ig20 FABRIC_COMMAND='sync_instance Customer.?';
</p>
<p>   
2) batchf Customer@DC1.batchFtest4() from HIS_DB using ('select patient_id from invoice where balance=12894') FABRIC_COMMAND='sync_instance Customer.?';
</p>
<p>
3) batchf Customer.batchFtest4().(‘1’,’2’,’3’) FABRIC_COMMAND='sync_instance Customer.?';
</p>
</td>
</tr> 
</table>

## Batch Commands Examples

### batch_list

Command  

``` batch_list status='all'```

Result 
```
|Id                                  |Command                                                                                                                                                                |Start date         |End date           |Status|Created by|Completion %|Error|
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-------------------+------+----------+------------+-----+
|35408af6-b26a-4243-bc95-f114335bfa5e|BATCH AUTODATA_DELTA FROM idsFile USING ('select id from ids  limit 200') FABRIC_COMMAND="sync_instance AUTODATA_DELTA.?" with JOB_AFFINITY='10.21.2.102' ASYNC='true';|2020-08-12 12:20:07|2020-08-12 12:20:09|DONE  |          |100         |null |
```


### batch_summary

Command 

``` batch_list status='all'```

Result

<img src="/articles/20_jobs_and_batch_services/images/22_jobs_and_batch_services_commandsExamples.PNG">

This command returns execution information and statistics for a given bid on each node in the execution:
- Name, the Node ID.
- %Completed, percentage of executions run on each node.
- Ent/sec, average entities executed per seconds (pace).

Note that all other fields are self-explanatory. 


## Instance Groups

### How Do I Create a New Instance Group?
1. Go to the **Fabric Studio**, select the **LU** > **Instance Groups** and right click and select **New Instance Group**.
2. Write a valid **SQL query** to select the instances to be included in the Instance Group.
3. Save the **Instance Group**.

<img src="/articles/20_jobs_and_batch_services/images/23_jobs_and_batch_services_commandsExamples.PNG">

The Instance Group (referred to as **customer_IG_600To700** in the screenshot above) is deployed together with its LUT.

### How Do I Invoke an Instance Group from the Batch Command

Example 

    batch Customer.customer_IG_600To700 FABRIC_COMMAND="sync_instance PATIENT.?" with JOB_AFFINITY='10.21.2.102' async='true';

The Instance Group is defined from Fabric Studio - *customer_IG_600To700*

Result 

All instances with ID values between 600 and 700 are synced into Fabric.

fabric>batch Customer.customer_IG_600To700 FABRIC_COMMAND="sync_instance PATIENT.?";
```
|Added|Updated|Unchanged|Failed|Total|Duration|
+-----+-------+---------+------+-----+--------+
|99   |0      |0        |0     |99   |875     |
```

## Batch Command with Embedded SQL Statements
Instead of referring to an Instance Group, the batch command can embed an SQL statement to select the entities on which the batch command is executed:
```
batch <LUT> from <db_interface> using ('<SQL>') fabric_command='<fabric command> ?'
```

Example 

fabric>batch Customer from CRM_DB USING('select customer_id from Customer where customer_id <=10') FABRIC_COMMAND="sync_instance CUSTOMER.?";
```
|Batch id                            |Execution succeeded|Execution failed|Total|Duration|Batch id                            |
+------------------------------------+-------------------+----------------+-----+--------+------------------------------------+
|83fade2f-2ae6-4359-8b7a-bdd1866d2191|10                 |0               |10   |1       |83fade2f-2ae6-4359-8b7a-bdd1866d2191|
```

## Legacy Support

### Migrate Commands
The Migrate command is a specific use-case of the Batch command which deals exclusively with the migration of instances into the Fabric database. 
Behind the scenes, Fabric activates the batch command when running the Migrate command. All the verbose defined for the batch process commands can be applied to the Migrate command without specifying the FABRIC_COMMAND parameter.

For example:
The following two commands are equivallent.

``` batch <LUT>[@<DC>] FABRIC_COMMAND='<fabric command> ?' ``` is the same as ```migrate <LUT>[@<DC>]```

Using the same example as above:
```
fabric>migrate Customer.customer_IG_600To700;
```
The results are the same as when running the batch command: 

```
batch Customer.customer_IG_600To700 FABRIC_COMMAND="sync_instance PATIENT.?";``` 
```
```

|Added|Updated|Unchanged|Failed|Total|Duration|
+-----+-------+---------+------+-----+--------+
|99   |0      |0        |0     |99   |875     |
```

### migratef Command 

The migratef command enables the migration of a selective list of instances using a function. 

<table width="900pxl">
<tbody>
<tr>
<td valign="top" width="300pxl">
<p><strong>Command Name</strong></p>
</td>
<td valign="top" width="400pxl">
<p><strong>Description</strong></p>
</td>
<td valign="top" width="300pxl">
<p><strong>Example</strong></p>
</td>
</tr>

<tr>
<td valign="top" width="500pxl">
<h5>
MigrateF – migrate a list of instances by function.
   
Use this command to migrate a selective list of instances defined by a function.</h5>
</td>
<td valign="top" width="400pxl">
   
<p>
1) migratef &ltLUT>[@&ltDC&gt].&ltfunction&gt().&ltIG&gt [WITH [AFFINITY='&ltaffinity&gt'] [JOB_AFFINITY='&ltjob affinity&gt'] [ASYNC=true/false] [GENERATE_IIDS_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];</p>

<p>2) migratef &ltLUT&gt[@&ltDC&gt].&ltfunction&gt() from &ltdb_interface&gt using ('&ltSQL&gt') [WITH [AFFINITY='&ltaffinity&gt'] [ASYNC=true/false] [GENERATE_IIDS_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];</p>
<p>  
3) migratef &ltLUT&gt[@&ltDC&gt].&ltfunction&gt().(&ltInstance 1, Instance 2, etc...&gt) [WITH [AFFINITY='&ltaffinity&gt'] [ASYNC=true/false] [GENERATE_IIDS_FIRST=true/false] [ALLOW_MULTIPLY=true/false] [MAX_NODES=&ltnumber&gt] [MAX_WORKERS_PER_NODE=&ltnumber&gt]];</p>
   
</td>
<td valign="top" width="300pxl">
<p>
1) migratef Customer.migrateFtest4().ig20;
</p>
<p>   
2) migratef Customer@DC1.migrateFtest4() from HIS_DB using ('select patient_id from invoice where balance=12894');
</p>
<p>
3) migratef Customer.migrateFtest4().(‘1’,’2’,’3’);
</p>
</td>
</tr>  


<tr>
<td valign="top" width="500pxl">
<h5>
migrate_resume '&ltmigrate id&gt';
</h5>
</td>
<td valign="top" width="400pxl">
   
<p>
Resumes a Migrate command by processing all failed or unhandled instances from previous executions.
</p>
   
</td>
<td valign="top" width="300pxl">
<p>
migrate_resume ‘161f9717-bd93-4882-a3aa-7b58c1f61b27’;
</p>
</td>
</tr>


</tbody>
</table>

[![Previous](/articles/images/Previous.png)](/articles/20_jobs_and_batch_services/07_batch_process_overview.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](/articles/20_jobs_and_batch_services/09_batch_process_flow.md)