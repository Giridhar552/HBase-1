# Existence of Table

You can verify the existence of a table using the exists command. For example:

``` Java
hbase(main):024:0> exists 'emp'
Table emp does exist

0 row(s) in 0.0750 seconds
```

## Verifying the Existence of Table Using Java API

You can verify the existence of a table in HBase using the **tableExists()** method of the **HBaseAdmin** class. Follow the steps 
given below to verify the existence of a table in HBase.

### Step 1

``` Java
Instantiate the HBaseAdimn class

// Instantiating configuration object
Configuration conf = HBaseConfiguration.create();

// Instantiating HBaseAdmin class
HBaseAdmin admin = new HBaseAdmin(conf); 
```

### Step 2

Verify the existence of the table using the **tableExists()** method.

Given below is the java program to test the existence of a table in HBase using java API.

### Complete program to check if a table exists in HBase using the java API

``` Java
import java.io.IOException;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class TableExists{

   public static void main(String args[])throws IOException{

      // Instantiating configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Verifying the existance of the table
      boolean bool = admin.tableExists("emp");
      System.out.println( bool);
   }
} 
```
