# Disabling a Table

## Disabling a Table using HBase Shell

To delete a table or change its settings, you need to first disable the table using the disable command. 
You can then re-enable it using the enable command.

Command to disable a table:

``` Java
disable 'emp'
```

### Verification

After disabling a table you can still sense its existence through ##list## and ##exists## commands. However you cannot scan it. For 
example:

``` Java
hbase(main):028:0> scan 'emp'
ROW         COLUMN + CELL
ERROR: emp is disabled.
```

### is_disable

This command is used to find whether a table is disabled

``` Java
hbase> is_disabled 'table name'
```

It will return true in case mps is disabled. If it is not disabled, it will return false.

``` Java
hbase(main):031:0> is_disabled 'emp'
true
0 row(s) in 0.0440 seconds
```

### disable_all

With this command you can disable all the tables maching the given regex.

``` Java
hbase(main):002:07> disable_all 'my_tab.*'
my_tab1
my_tab2
my_tab3
my_tab4
my_tab5
Disable the above 5 tables (y/n)?
y
5 tables successfully disabled
```

## Disable a Table Using Java API

To verify whether a table is disabled, **isTableDisabled()** method is used and to disable a table, **disableTable()**
method is used. These methods belong to the **HBaseAdmin** class. Follow the steps given below to disable a table.

### Step 1

Instantiate HBaseAdmin class

``` Java
// Creating configuration object
Configuration conf = HBaseConfiguration.create();

// Creating HBaseAdmin object
HBaseAdmin admin = new HBaseAdmin(conf);
```

### Step 2

Verify whether the table is disabled using **isTableDisabled()** method as shown below.

``` Java
Boolean b = admin.isTableDisabled("emp");
```

### Step 3

If the table is not disabled, disable it as shown below

``` Java
if(!b){
   admin.disableTable("emp");
   System.out.println("Table disabled");
}
```

### Complete code

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.MasterNotRunningException;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class DisableTable{

   public static void main(String args[]) throws MasterNotRunningException, IOException{

      // Instantiating configuration class
      Configuration conf = HBaseConfiguration.create();
 
      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Verifying weather the table is disabled
      Boolean bool = admin.isTableDisabled("emp");
      System.out.println(bool);

      // Disabling the table using HBaseAdmin object
      if(!bool){
         admin.disableTable("emp");
         System.out.println("Table disabled");
      }
   }
}
```

