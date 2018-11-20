## Creating and Inserting values into a table at the column level

### Configuring HBase path

When we create HBase configuration, it will point to whatever the configurations we set in hbase-site.xml and hbase-default.xml files during HBase installations

``` HBase
org.apache.hadoop.conf.Configurationconfig config = HBaseConfiguration.create();
```

### Table myTable creation

Creating a Table using HTable method

```HBase
HTable table = new HTable(config, "myTable");
```

### Adding row1 to myTable

```HBase
Put p = new Put(Bytes.toBytes("row1"));
```

### Inserting values into column

Specifying column names "education" and "projects" and inserting values into column names in the respective row1. The values inserted here are "BigData" and "HBaseTutorials".

```HBase
p.add(Bytes.toBytes("education"), Bytes.toBytes("col1"), Bytes.toBytes("BigData"));
p.add(Bytes.toBytes("projects"), Bytes.toBytes("col2"), Bytes.toBytes("HBaseTutorials"));
```
