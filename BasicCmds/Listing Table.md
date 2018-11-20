#Listing Tables

## Listing a Table using HBase Shell

To list all the tables in HBase use the list() command

> List

## Listing Tables using Java API

### Step 1

You have a method called **listTables()** in the class **HBaseAdmin** to get the list of all the tables in HBase. This method returns 
an array of the **HTableDescriptor** objects.

``` Java
//creating a configuration object
Configuration conf = HBaseConfiguration.create();

//Creating HBaseAdmin object
HBaseAdmin admin = new HBaseAdmin(conf);

//Getting all the list of tables using HBaseAdmin object
HTableDescriptor[] tableDescriptor = admin.listTables();
```

### Step 2

You can get the length of the **HTableDescriptor[]** array using the lenght variable of the **HTableDescriptor** class. Get the name of 
the tables from this object using **getNameAsString()** method.

### Complete code

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.MasterNotRunningException;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class ListTables {

   public static void main(String args[])throws MasterNotRunningException, IOException{

      // Instantiating a configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Getting all the list of tables using HBaseAdmin object
      HTableDescriptor[] tableDescriptor = admin.listTables();

      // printing all the table names.
      for (int i=0; i<tableDescriptor.length;i++ ){
         System.out.println(tableDescriptor[i].getNameAsString());
      }
   
   }
}
```
