# Inserting Data using HBase

To create data in an HBase table the following commands and methods are used:

* **put** command
* **add()** method, which belongs to **Put** class
* **put()** method, which belongs to **HTable** class

Using **put** you can insert rows into a table. Its syntax is as follows:

``` Java
put ’<table name>’,’row1’,’<colfamily:colname>’,’<value>’
```

### Inserting the First Row

To insert the first row value into the empt table as shown below

``` Java
hbase(main):005:0> put 'emp','1','personal data:name','raju'
0 row(s) in 0.6600 seconds
hbase(main):006:0> put 'emp','1','personal data:city','hyderabad'
0 row(s) in 0.0410 seconds
hbase(main):007:0> put 'emp','1','professional
data:designation','manager'
0 row(s) in 0.0240 seconds
hbase(main):007:0> put 'emp','1','professional data:salary','50000'
0 row(s) in 0.0240 seconds
```

## Inserting Data using Java API

You can insert data into Hbase using the **add()** method of the **Put** class. You can save it using the **put()** method of the 
**HTable** class. These classes belong to the **org.apache.hadoop.hbase.client** package. Below given are the steps to create data 
in a Table of HBase.

### Step 1: Instantiate the Configuration Class

The **Configuration** class adds HBase configuration files to its object. You can create a configuration object using the **create()** 
method of the **HbaseConfiguration** class as shown below.

``` Java
Configuration conf = HbaseConfiguration.create();
```

### Step 2:Instantiate the HTable Class

You have a class called HTable, an implementation of Table in **HBase**. This class is used to communicate with a single HBase 
table. While instantiating this class, it accepts configuration object and table name as parameters. You can instantiate HTable 
class as shown below.

``` Java
HTable hTable = new HTable(conf, tableName);
```

### Step 3: Instantiate the PutClass

To insert data into an HBase table, the add() method and its variants are used. This method belongs to Put, therefore instantiate 
the put class. This class requires the row name you want to insert the data into, in string format. You can instantiate the Put 
class as shown below.

``` Java
Put p = new Put(Bytes.toBytes("row1"));
```

### Step 4: Insert Data

The add() method of Put class is used to insert data. It requires 3 byte arrays representing column family, column qualifier 
(column name), and the value to be inserted, respectively. Insert data into the HBase table using the add() method as shown below.

``` Java
p.add(Bytes.toBytes("coloumn family "), Bytes.toBytes("column name"),Bytes.toBytes("value"));
```


### Step 5: Save the Data in Table

After inserting the required rows, save the changes by adding the put instance to the put() method of HTable class as shown below.

``` Java
hTable.put(p); 
```

### Step 6: Close the HTable Instance

After creating data in the HBase Table, close the HTable instance using the close() method as shown below.

``` Java
hTable.close(); 
```

### The complete program to insert Data

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.client.HTable;
import org.apache.hadoop.hbase.client.Put;
import org.apache.hadoop.hbase.util.Bytes;

public class InsertData{

   public static void main(String[] args) throws IOException {

      // Instantiating Configuration class
      Configuration config = HBaseConfiguration.create();

      // Instantiating HTable class
      HTable hTable = new HTable(config, "emp");

      // Instantiating Put class
      // accepts a row name.
      Put p = new Put(Bytes.toBytes("row1")); 

      // adding values using add() method
      // accepts column family name, qualifier/row name ,value
      p.add(Bytes.toBytes("personal"),
      Bytes.toBytes("name"),Bytes.toBytes("raju"));

      p.add(Bytes.toBytes("personal"),
      Bytes.toBytes("city"),Bytes.toBytes("hyderabad"));

      p.add(Bytes.toBytes("professional"),Bytes.toBytes("designation"),
      Bytes.toBytes("manager"));

      p.add(Bytes.toBytes("professional"),Bytes.toBytes("salary"),
      Bytes.toBytes("50000"));
      
      // Saving the put Instance to the HTable.
      hTable.put(p);
      System.out.println("data inserted");
      
      // closing HTable
      hTable.close();
   }
}
```

