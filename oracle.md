# Definition:
<br>
* An Oracle database is a collection of data treated unit. The purpose of Oracle is to store and retrieve related information.
* in general, a database manages a large amount of data so many users can use it concurrently access the same data.With high performence.
* also prevents unauthorized access.
* the database has a logical and a physical structure.



# Architecture overview:
<br><br>
*   *Physical memory structure*
   
    Data file, control file, redo log file
   
    *These files are created by the CREATE DATABASE*

*   Database objects are stored in the Data files which the end user and the programmer work with.

    * Tables
    * Indices
    * Cluster
    * Rollback segments
<br><br>
 _These files takes memory space that has a specific logical structure on it._
<br><br><br>

*   Logical memory structure
    Data block, extent, segment, tablespace
    These constructs are only known to Oracle - but not
    the operating system
<br><br><br>

# Oracle application system:
<br><br>
*  Application system
<br><br>
* Database management system

    * Oracle core
        * controls and executes all database operations.
    * System Global Area
        * is the communication area between DBMS and application programs.
    * Background processes
<br><br>
* Database: disk storage areas where the actual data is stored

    * REDO log files for DB recovery
        * at least 2 per DB.
    * Control files for DB system administration
        * at least 2, which should be stored on different disks.
   
<br><br><br>

# Logical structure - Tablespace:

<br><br>

*So what we already heard data objects are stored in data files and data files again are split in tablespaces.*

    * each tablespace can store any number of data objects.
    * A tablespace can be considered as a container for database objects such as tables, indexes,   etc.
    * a tablespace is assigned to one or more datafiles.
    * THE SYSTEM-TABLESPACE is only for system-relevant data.


![Database](image1.png)
<br><br><br>

# System Tablespace:

<br><br>

* Is created automatically when the database is created. It contains the data dictionary, tables and views with administrative information, compiled objects.

* The owner of all these objects is the SYS user.

* SYSTEM - Tablespace objects cannot be deleted or renamed.

<br><br><br>

# Enlargement of a tablespace:

<br><br>


![System Tablespace](image2.png)

![Enlargement of a tablespace](image3.png)

* Tables can be split to different tablespaces and to different files:

    * frequently used tables on fast memory, rarely used tables on slow memory.
    * tables that are frequently used for JOINS can be stored on different disks.

* if a tablespace contains files from several disks, a table can also grow across disk boundaries.

<br><br><br>

# Tablespace:

<br><br>

* The SYSTEM tablespace is created when the database is created. It must be present because ->

    * The SYSTEM tablespace contains the data dictionary tables.

    * The SYSTEM tablespace and the ROLLBACK tablespace must not be lost under any circumstances. There is no possibility to start the database without these tablespaces.

* Optimally a tablespace consists of a database file. If necessary, further database files can be added to a tablespace.

* Also tablespaces can be put offline. (Tablespace backup, reorganization, addition of database files etc.).

* Each Oracle user is assigned a default and temporary tablespace.

* User data should never be created in the SYSTEM tablespace.

* The SYSAUX - TableSpace extends the functionality of the SYSTEM - TableSpace

<br><br><br>

# Tablespace:

<br><br>

* User data in user tablespace

    * = Default tablespace for user tables. Each user is assigned this tablespace to store their data. For optimal performance, no index segments should be created in this tablespace.

* Indexes

    * The index tablespace contains the indexes of the user tables. For optimal performance, no tables should be created in this tablespace.

* SYSTEM

    * The SYSTEM tablespace must always be available, because it contains the online data dictionary with the locations of all database objects. If the SYSTEM tablespace is lost, the database can no longer be started. It also contains compiled objects such as triggers, procedures and functions.

* Rollback

    * The rollback segment tablespace contains the private rollback segments. Rollback segments ensure read consistency at the transaction and command levels.

* Temporary Data

    * In the Temporary tablespace, Oracle performs sort operations internally (SELECT .... ORDER BY). Temporary segments are created and deleted dynamically. They are not under the control of the user processes.
