# Enabling a Table

## Enabling a Table using HBase

Command to enable a table

``` Java
enable 'emp'
```

### Verification

``` Java
hbase(main):006:0> scan 'emp'

   ROW                        COLUMN + CELL

1 column = personal data:city, timestamp = 1417516501, value = hyderabad

1 column = personal data:name, timestamp = 1417525058, value = ramu

1 column = professional data:designation, timestamp = 1417532601, value = manager

1 column = professional data:salary, timestamp = 1417524244109, value = 50000
...
```

### is_enabled

This command is used to find whether a table is enabled

``` Java
hbase> is_enabled 'table name'
```

If the table is enabled, it will return true and if not, it will return false

``` Java
hbase(main):031:0> is_enabled 'emp'
true
0 row(s) in 0.0440 seconds
```

## Enable a Table using Java API

To verify whether a table is enabled, **isTableEnabled()** method is used; and to enable a table, **enableTable()** method is used. 
These methods belong to **HBaseAdmin** class. Follow the steps given below to enable a table.

### Step 1

Instantiate HBaseAdmin class as shown below

``` Java
// Creating configuration object
Configuration conf = HBaseConfiguration.create();

// Creating HBaseAdmin object
HBaseAdmin admin = new HBaseAdmin(conf);
```

### Step 2

Verify whether the table is enabled using **isTableEnabled()** method as shown below

``` Java
Boolean bool = admin.isTableEnabled("emp");
```

### Step 3

If the table is not disabled, disable it as shown below

``` Java
if(!bool){
   admin.enableTable("emp");
   System.out.println("Table enabled");
}
```

### Complete script

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.MasterNotRunningException;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class EnableTable{

   public static void main(String args[]) throws MasterNotRunningException, IOException{

      // Instantiating configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Verifying whether the table is disabled
      Boolean bool = admin.isTableEnabled("emp");
      System.out.println(bool);

      // Enabling the table using HBaseAdmin object
      if(!bool){
         admin.enableTable("emp");
         System.out.println("Table Enabled");
      }
   }
}
```

