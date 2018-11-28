### What is HBase

* It is a **distributed column-oriented database** built **on top of the Hadoop** file system. 

* It is horizontally scalable.

* It is a data model similar to Google’s big table, designed to provide quick random access to huge amounts of structured data. 
 
* It leverages the fault tolerance provided by the Hadoop File System (HDFS).

* It is a part of the Hadoop ecosystem

* It provides random real-time read/write access to data in the Hadoop File System.

* It is possible to store the data in HDFS either directly or through HBase. 

* Data consumer reads/accesses the data in HDFS randomly using HBase. 


### HBase Vs. HDFS

**HDFS**

* HDFS is a distributed file system suitable for storing large files.	
* HDFS does not support fast individual record lookups.	
* HDFS provides high latency batch processing; no concept of batch processing.	
* HDFS provides only sequential access of data.	

**HBase**

* HBase is a database built on top of the HDFS.
* HBase provides fast lookups for larger tables.
* HBase provides low latency access to single rows from billions of records (Random access).
* HBase internally uses Hash tables and provides random access, and it stores the data in indexed HDFS files for faster lookups.


**Storage Mechanism in HBase**

HBase is a column-oriented database and the tables in it are sorted by row. The table schema defines only column families, which 
are the key value pairs. 

A table have multiple column families and each column family can have any number of columns. Subsequent column values are stored 
contiguously on the disk. Each cell value of the table has a timestamp. 

In short, in an HBase:

* Table is a collection of rows.
* Row is a collection of column families.
* Column family is a collection of columns.
* Column is a collection of key value pairs.

### Column Oriented Vs. Row Oriented

Column-oriented databases are those that store data tables as sections of columns of data, rather than as rows of data. 
Shortly, they will have column families.

**Row-Oriented Database**

* It is suitable for Online Transaction Process (OLTP)
* Such databases are designed for small number of rows and columns.	
* Can write data very quickly

**Column-Oriented Database**

*	It is suitable for highly analytical query model  (Online Analytical Processing, OLAP).
* Can aggregate large volumes of data for a subset of columns.
* Can query data really fast. So they are a good choice in a query-heavy environment. But you must ensure 
  that the queries you run are really suited to a columnar database.


### Features of HBase

* It is linearly scalable.
* It has automatic failure support.
* It provides consistent read and writes.
* It integrates with Hadoop, both as a source and a destination.
* It has easy java API for client.
* It provides data replication across clusters.

### Where to Use HBase

* Apache HBase is used to have random, real-time read/write access to Big Data.
* It hosts very large tables on top of clusters of commodity hardware.
* Apache HBase is a non-relational database modeled after Google's Bigtable. Bigtable acts up on Google File System, likewise Apache HBase works on top of Hadoop and HDFS.

### Applications of HBase

* It is used whenever there is a need to write heavy applications.
* HBase is used whenever we need to provide fast random access to available data.
* Companies such as Facebook, Twitter, Yahoo, and Adobe use HBase internally.


## Further information

### Data Storage example basic database.

The database is a stockbroker’s transaction records. 

**Row-oriented database**

* There will one table named customer. **Each customer** would have **one single record** with their basic information: 
  name, address, phone number, etc. It’s likely that each record would have a unique identifier, for example *account_number*.

* There is another table that stores stock transactions. Each transaction is uniquely identified by something like a 
transaction_id. Each transaction is associated to one *account_number*, but each **account_number** is **associated** with **multiple 
transactions**. This provides us with a **one-to-many relationship** and is a classic example of a transactional database.

We store all these tables on a disk and, when we run a query, the system might access lots of data before it determines what 
information is relevant to the specific query. 

For example, let imagine that we want to know the account_number, first_name, last_name, stock, and purchase_price for a given time period. 

* First the system needs to access all of the information for the two tables, including fields that may not be relevant to the query. 
* Second it performs a join to relate the two tables’ data, and then it can return the information. 


**Columna-oriented database**

**Each field from each table is stored in its own file** or set of files. In our example database, **all account_number data is stored 
in one file**, **all transaction_id data** is stored **in another file**, and so on. 

This provides some efficiencies when running queries against wide tables, since it is unlikely that a query needs to return all of the 
fields in a single table. 

In the **query** example **above**, we’d only need to **access the files that contained data** from the requested fields. You can **ignore all other fields** that exist in the table. This ability to minimize i/o is one of the key reasons columnar databases can perform much 
faster.

### Normalization Versus Denormalization

Many columnar databases prefer a **denormalized data structure**. In the example above, we have **two separate tables**: one for account information and one for transaction information. In many **columnar databases**, a **single table could represent this information instead of two separate tables**. With this denormalized design, when a query like the one presented is run, **no joins** would need to be processed in the columnar database, so the **query** will likely run **much faster**.

The reason for **normalizing data** is that it **allows data to be written to the database in a highly efficient manner**. In our **row store example, we need to record just the relevant transaction details** whenever an existing customer makes a transaction. The account information does not need to be written along with the transaction data. Instead, we reference the account_number to gain access to all of the fields in the accounts table.

**Normalization** of data also **makes updates** to some information much **more efficient** in a **row-oriented**. If you **change an account holder’s address, you simply update the one record in the accounts table**. The updated information is available to all transactions completed by that account owner. In the **columnar database**, since **we might store the account information with the transactions** of that user, **many records might need updating** in order update the available address information.



Sources:

https://dzone.com/articles/row-store-and-column-store-databases
https://www.tutorialspoint.com/hbase/hbase_overview.htm

