# SQL

Find DB raw size
``` sql
SELECT INTERVAL_START,RAW_OBJECT_SIZE_AVG FROM EXA_STATISTICS.EXA_DB_SIZE_DAILY order by interval_start desc limit 1;
or
SELECT * FROM EXA_STATISTICS.EXA_DB_SIZE_DAILY order by interval_start desc limit 1;
```
Find recommended DB RAM size
``` sql
select INTERVAL_START,RECOMMENDED_DB_RAM_SIZE_AVG FROM EXA_STATISTICS.EXA_DB_SIZE_MONTHLY order by interval_start desc limit 10;
```
Check what is running right now
``` sql
select * from "$EXA_PROFILE_RUNNING" order by duration desc;
```
Check when the database version was updated or DB RAM/parameter CHANGE
``` sql
SELECT max(measure_time) AS "WHEN", dbms_version AS "VERSION", db_ram_size, parameters
  FROM exa_system_events s
  WHERE event_type = 'STARTUP'
  GROUP BY dbms_version, db_ram_size, parameters
  ORDER BY LOCAL."WHEN" DESC;
```
Create a connection
``` sql
CREATE CONNECTION mysql_con TO 'jdbc:mysql://192.168.6.1'
                            USER 'my_user'
                            IDENTIFIED BY 'my_pw';
```
Create a table
``` sql
CREATE TABLE customers (firstname VARCHAR (200),
                        lastname VARCHAR (200),
                        birthday DATE);
```
Import data
``` sql
IMPORT INTO customers FROM jdbc AT mysql_con TABLE customers;
```
Check what kind of DB profile is running
``` sql
select * from EXA_DBA_PROFILE_RUNNING where session_id!=current_session;
```
Find out how much DB RAM is allocated to the DB
``` sql
select * from EXA_SYSTEM_EVENTS order by 2 desc;
```

# SYSTEM TABLES
``` sql
select * from exa_syscat;					    --- Check the existing database tables for system and statistic information
select * from exa_dba_sessions;					--- Check the ongoing sessions connected to the database
select * from exa_metadata where param_name like 'database%';	--- Check the most important database attributes:
select * from exa_parameters;					--- Check the database parameters, configurable on system and session layer
select * from exa_system_events;				--- Check the system events
select * from exa_system_events order by 2 desc limit 20;	    --- Check the system events
export (select * from exa_system_events order by 2 desc limit 20) into local csv file '/home/bomi/sys_events.csv' with column names; --- Export the system events in local CSV file
select CURRENT_TIMESTAMP;                       --- Check the current timestamp from DB point of view
```

# USERS and PRIVILEGES 
``` sql
create user user1 identified by "user1";	        --- As the sys user, create a new user named user1
grant create session to user1;			            --- Allow that user to connect to the database
create role role1;				                    --- Create a new role named role1
grant create schema,create table to role1;	        --- Grant the system privileges needed to create schemas and tables to that role
grant role1 to user1;				                --- Grant that role to user1
connect user1/user1;				                --- Connect as user1 to the database
create schema user1;				                --- Create a new schema as that user:
create table t1 as select * from exa_session_privs;	--- Create a table within that schema for that user
select * from exa_user_tables;			            --- Check metainfo of your tables:
```

# SCHEMAS
``` sql
CREATE SCHEMA IF NOT EXISTS schema_name;		    --- Create a new schema
ALTER SCHEMA schema_name CHANGE OWNER user_or_role	--- Change owner of schema
DROP SCHEMA IF EXISTS schema_name [CASCADE];
```
Export a table into a local CSV file
``` sql
export (select * from exa_dba_schemas) into local csv file 'O:\schemas.csv' with column names;
```
Audit hast to be enabled. Check the performance hogs by DURATION
``` sql
select * from "EXA_STATISTICS"."EXA_DBA_AUDIT_SQL" where start_time > '2022-05-29 17:12:00' and stop_time < '2022-05-30 17:12:00' order by DURATION desc limit 20;
```
Same as above but selecting custom columns
``` sql
select session_id, command_name, duration, start_time, stop_time, temp_db_ram_peak, persistent_db_ram_peak, SQL_TEXT from "EXA_STATISTICS"."EXA_DBA_AUDIT_SQL" where start_time > '2022-05-29 17:12:00' and stop_time < '2022-05-30 17:12:00' order by DURATION desc limit 20;
```
