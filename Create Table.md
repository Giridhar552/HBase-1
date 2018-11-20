# Creating a Table in HBase

## Creating a Table using HBase Shell

``` Java
create '<table name>', '<column family>'
```

If we want to create a table named *emp* with two column families: *personal data* and *professional data*, then we should write:

``` Java
> create 'emp', 'personal data', 'professional data'
```

It will return the following output

``` Java
0 row(s) in 1.1300 seconds
=> Hbase::Table - emp
```

### Verification

``` Java
> list
TABLE
emp
2 row(s) in 0.0340 seconds
```

## Creating a Table using java API

You can create a table in HBase using the createTable() method of HBaseAdmin class. This class belongs to the **org.apache.hadoop.hbase.client package**

### Step 1: Instantiate HBaseAdmin

``` Java
Configuration conf = HBaseConfiguration.create();
HBaseAdmin admin = new HBaseAdmn(conf);
```
