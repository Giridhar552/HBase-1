# Describe

This command returns the description of the table

``` Java
hbase> describe 'table name'
```

For example

``` Java
hbase(main):006:0> describe 'emp'
   DESCRIPTION
      ENABLED
      
'emp', {NAME ⇒ 'READONLY', DATA_BLOCK_ENCODING ⇒ 'NONE', BLOOMFILTER
⇒ 'ROW', REPLICATION_SCOPE ⇒ '0', COMPRESSION ⇒ 'NONE', VERSIONS ⇒
'1', TTL true

...

```

# alter

Alter is the command used to make changes to an existing table. Using this command, you can change the maximum number of cells of a 
column family, set and delete table scope operators, and delete a column family from a table.

### Changing the Maximum Number of Cells of a Column Family

Syntax to change the maximun number of cells of a column family. If we want to set the maximun number of cells to 5

``` Java
hbase(main):003:0> alter 'emp', NAME ⇒ 'personal data', VERSIONS ⇒ 5
Updating all regions with the new schema...
0/1 regions updated.
1/1 regions updated.
Done.
0 row(s) in 2.3050 seconds
```

### Table Scope Operators

Using alter, you can set and remove table scope operators such as MAX_FILESIZE, READONLY, MEMSTORE_FLUSHSIZE, DEFERRED_LOG_FLUSH, etc.

### Setting Read Only

Use the below command to make a table read only

``` Java
hbase(main):006:0> alter 'emp', READONLY
Updating all regions with the new schema...
0/1 regions updated.
1/1 regions updated.
Done.
0 row(s) in 2.2140 seconds
```

### Removing Table Scope Operators

Below is the syntax to remove 'MAX_FILESIZE' from emp table

``` Java
hbase> alter 't1', METHOD ⇒ 'table_att_unset', NAME ⇒ 'MAX_FILESIZE'
```

### Deleting a Column Family

``` Java
hbase> alter ‘ table name ’, ‘delete’ ⇒ ‘ column family ’ 
```

For example:

``` Java
hbase(main):006:0> scan 'employee'

   ROW                   COLUMN+CELL

row1 column = personal:city, timestamp = 1418193767, value = hyderabad

row1 column = personal:name, timestamp = 1418193806767, value = raju

row1 column = professional:designation, timestamp = 1418193767, value = manager

row1 column = professional:salary, timestamp = 1418193806767, value = 50000

1 row(s) in 0.0160 seconds 
```

Now we will remove the column family named professional

``` Java
hbase(main):007:0> alter 'employee','delete'⇒'professional'
Updating all regions with the new schema...
0/1 regions updated.
1/1 regions updated.
Done.
0 row(s) in 2.2380 seconds 
```

We can see how the professional family column is gone

``` Java
hbase(main):003:0> scan 'employee'
   ROW             COLUMN + CELL
row1 column = personal:city, timestamp = 14181936767, value = hyderabad

row1 column = personal:name, timestamp = 1418193806767, value = raju

1 row(s) in 0.0830 seconds
```

## Adding a Column Family Using Java API

It is possible to add a column family to a table using the method **addColumn()** of **HBAseAdmin** class. Follow the steps given below to add a column family to a table.

### Step 1

Instantiate the **HBaseAdmin** class

``` Java
// Instantiating configuration object
Configuration conf = HBaseConfiguration.create();

// Instantiating HBaseAdmin class
HBaseAdmin admin = new HBaseAdmin(conf); 
```
### Step 2

The **addColumn()** method requires a table name and an object of **HColumnDescriptor** class. Therefore instantiate the **HColumnDescriptor** class. The constructor of **HColumnDescriptor** in turn requires a column family name that is to be added. Here we are adding a column family named “contactDetails” to the existing “employee” table.

``` Java
// Instantiating columnDescriptor object

HColumnDescriptor columnDescriptor = new HColumnDescriptor("contactDetails");
```

### Step 3

Add the column family using **addColumn** method. Pass the table name and the **HColumnDescriptor** class object as parameters to this method.

``` Java
// Adding column family
admin.addColumn("employee", new HColumnDescriptor("columnDescriptor"));
```

### Complete programm to add a column family to an existing table

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.MasterNotRunningException;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class AddColoumn{

   public static void main(String args[]) throws MasterNotRunningException, IOException{

      // Instantiating configuration class.
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class.
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Instantiating columnDescriptor class
      HColumnDescriptor columnDescriptor = new HColumnDescriptor("contactDetails");
      
      // Adding column family
      admin.addColumn("employee", columnDescriptor);
      System.out.println("coloumn added");
   }
}
```

## Deleting a Column Family using Java API

You can delete a column family from a table using the method **deleteColumn()** of **HBAseAdmin** class. Follow the steps given below to add a column family to a table.

### Step 1

Instantiate the HBaseAdmin class

``` Java
// Instantiating configuration object
Configuration conf = HBaseConfiguration.create();

// Instantiating HBaseAdmin class
HBaseAdmin admin = new HBaseAdmin(conf); 
```

### Step 2

Delete the column family using deleteColumn() method. Pass the table name and the column family name as parameters to this method.

``` Java
// Deleting column family
admin.deleteColumn("employee", "contactDetails"); 
```

### Full code

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.MasterNotRunningException;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class DeleteColoumn{

   public static void main(String args[]) throws MasterNotRunningException, IOException{

      // Instantiating configuration class.
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class.
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Deleting a column family
      admin.deleteColumn("employee","contactDetails");
      System.out.println("coloumn deleted"); 
   }
}
```

