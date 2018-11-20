# Dropping a Table

## Dropping a Table using HBase shell

Before dropping a table you need to disable it

``` Java
hbase(main):018:0> disable 'emp'
0 row(s) in 1.4580 seconds

hbase(main):019:0> drop 'emp'
0 row(s) in 0.3060 seconds
```

You can later verify if it exists or not

``` Java
hbase(main)>exists 'emp'
Table emp does not exist
0 row(s) in 0.0730 seconds
```

### drop_all

This command is used to drop the tables matching the "regex" given in the command. Its syntx is the following:

``` Java
hbase> drop_all ‘t.*’ 
```

For example:

Listing all the tables in HBase

``` Java
hbase(main):017:0> list
TABLE
tab1
tab2
tab3
tab4
tab5
9 row(s) in 0.0270 seconds
```

Disabling all tables which start with tab (actually the 5 we have got)

``` Java
hbase(main):002:0> disable_all 'tab.*'
tab1
tab2
tab3
tab4
tab5
Disable the above 5 tables (y/n)?
y
5 tables successfully disabled
```

Dropping all the tables which start with tab

``` Java
hbase(main):002:0> drop_all  'tab.*'
tab1
tab2
tab3
tab4
tab5
Drop the above 5 tables (y/n)?
y
5 tables successfully disabled
```

## Deleting a Table Using Java API

You can delete a table using the **deleteTable()** method in the **HBaseAdmin** class. Follow the steps given below to delete a 
table using java API.

### Step 1
Instantiate the HBaseAdmin class.

``` Java
// creating a configuration object
Configuration conf = HBaseConfiguration.create();

// Creating HBaseAdmin object
HBaseAdmin admin = new HBaseAdmin(conf); 
```

### Step 2
Disable the table using the **disableTable()** method of the **HBaseAdmin** class.

``` Java
admin.disableTable("emp2");
```

### Step 3
Now delete the table using the **deleteTable()** method of the **HBaseAdmin** class.

``` Java
admin.deleteTable("emp2");
```

### Complete Java program to delete a table in HBase.

``` Java
import java.io.IOException;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class DeleteTable {

   public static void main(String[] args) throws IOException {

      // Instantiating configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // disabling table named emp
      admin.disableTable("emp2");

      // Deleting emp
      admin.deleteTable("emp2");
      System.out.println("Table deleted");
   }
}
```
