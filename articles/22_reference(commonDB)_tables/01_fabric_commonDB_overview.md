# **Fabric CommonDB and Reference Overview** 


# **What are Reference (Common) Tables ?** 

A Reference table is an SQLite table containing metadata that is referenced by different LU instances of a specific LU, by instances from a different LU, by a web service, or by any other Fabric object (jobs, broadway flows, ...) .

For example, a Reference Table could be:
- a table storing a list of objects to which all MicroDB Schemas point to, 
- detailed information about a specific set of services to which all LUIs subscribe, 
- a geo-code table that identifies customer zip addresses, 
- a report of number of customers per customer type. 

In Fabric Studio, the Reference tab displays a list of the common Reference tables defined in a project.
To ensure that a Reference table in an LU Schema is always synched, verify that the Reference table name is checked in the References section of the LU Schema tab in the right pane.

When Fabric synchronizes any LU instance, it first searches for the checked Reference tables, checks if they need to be synchronized and then synchronizes them. 


# **Where are Reference Tables Stored ?**

CommonDB is an additional SQLite database used for storing reference tables common to all LUIs (MicroDBs).

In a distributed system, a copy of the CommonDB is stored on each Fabric node that is involved.
Fabric handles their cross-synchronization and ensures that the local CommonDB SQLite file is always available for queries from within each Fabric session. 
This enables writing JOIN clauses, locally, between any common table and any LUI using only one SQL query, thus providing instantenous data access and computing resources to these queries. 


 
[<img align="right" width="60" height="54" src="/articles/images/Next.png">](/articles/22_reference%28commonDB%29_tables/02_add_a_reference_table.md) 
