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

### Step 2: Create TableDescriptor

**HTableDescriptor** is a class that belongs to the **org.apache.hadoop.hbase** class. This class is like a container of table 
names and column families

``` Java
//creating table descriptor
HTableDescriptor table = new HTableDescriptor(toBytes("Table name"));

//creating column family descriptor
HColumnDescriptor family = new HColumnDescriptor(toBytes("column family"));

//adding coloumn family to HTable
table.addFamily(family);
```

### Step 3: Execute through Admin

Using the createTable() method of HBaseAdmin class, you can execute the created table in Admin mode.

``` Java
admin.createTable(table);
```

### Complete code to create table via admin


``` Java
import java.io.IOException;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.client.HBaseAdmin;
import org.apache.hadoop.hbase.TableName;

import org.apache.hadoop.conf.Configuration;

public class CreateTable {
      
   public static void main(String[] args) throws IOException {

      // Instantiating configuration class
      Configuration con = HBaseConfiguration.create();

      // Instantiating HbaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(con);

      // Instantiating table descriptor class
      HTableDescriptor tableDescriptor = new
      HTableDescriptor(TableName.valueOf("emp"));

      // Adding column families to table descriptor
      tableDescriptor.addFamily(new HColumnDescriptor("personal"));
      tableDescriptor.addFamily(new HColumnDescriptor("professional"));

      // Execute the table through admin
      admin.createTable(tableDescriptor);
      System.out.println(" Table created ");
   }
}
```


