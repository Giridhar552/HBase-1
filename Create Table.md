# Creating a Table in HBase

### Creating a Table using HBase Shell

  create '<table name>', '<column family>'

If we want to create a table named *emp* with two column families: *personal data* and *professional data*, then we should write:

``` HBase
> create 'emp', 'personal data', 'professional data'
```

It will retrieve the following output

``` HBase
0 row(s) in 1.1300 seconds
=> Hbase::Table - emp
```
