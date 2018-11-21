# Deleting a specific Cell in a Table

Using the **delete** command, you can delete a specific cell in a table. The syntax of **delete** command is as follows:

``` Java
delete ‘<table name>’, ‘<row>’, ‘<column name >’, ‘<time stamp>’
```

Example

``` Java
hbase(main):006:0> delete 'emp', '1', 'personal data:city',
1417521848375
0 row(s) in 0.0060 seconds
```

### Deleting All Cells in a Table

Using the **deleteall** command, you can delete all the cells in a row. Given below is the syntax of deleteall command.

``` Java
deleteall ‘<table name>’, ‘<row>’,
```

Example

``` Java
hbase(main):007:0> deleteall 'emp','1'
0 row(s) in 0.0240 seconds
```

## Deleting Data Using Java API

You can delete data from an HBase table using the **delete()** method of the **HTable** class. Follow the steps given below to delete data from a table.

### Step 1: Instantiate the Configuration Class

**Configuration** class adds HBase configuration files to its object. You can create a configuration object using the **create()** method of the the **HbaseConfiguration** class as shown below.

``` Java
Configuration conf = HbaseConfiguration.create();
```

### Step 2: Instantiate the HTable Class

You have a class called **HTable**, an implementation of Table in HBase. This class is used to communicate with a single HBase table. While instantiating this class, it accepts the configuration object and the table name as parameters. You can instantiate the HTable class as shown below.

``` Java
HTable hTable = new HTable(conf, tableName); 
```

### Step 3: Instantiate the Delete Class

Instantiate the Delete class by passing the rowid of the row that is to be deleted, in byte array format. You can also pass timestamp and Rowlock to this constructor.

``` Java
Delete delete = new Delete(toBytes("row1"));
```

### Step 4: Select the Data to be Deleted

You can delete the data using the **delete** methods of the **Delete** class. This class has various delete methods. Choose the columns or column families to be deleted using those methods. Take a look at the following examples that show the usage of Delete class methods.

``` Java
delete.deleteColumn(Bytes.toBytes("personal"), Bytes.toBytes("name"));
delete.deleteFamily(Bytes.toBytes("professional"));
```

### Step 5: Delete the Data

Delete the selected data by passing the **delete** instance to the **delete()** method of the **HTable** class as shown below.

``` Java
table.delete(delete); 
```

### Step 6: Close the HTableInstance

After deleting the data, close the HTable Instance.

``` Java
table.close();
```


### Complete Program to Delete Data


``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.client.Delete;
import org.apache.hadoop.hbase.client.HTable;
import org.apache.hadoop.hbase.util.Bytes;

public class DeleteData {

   public static void main(String[] args) throws IOException {

      // Instantiating Configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HTable class
      HTable table = new HTable(conf, "employee");

      // Instantiating Delete class
      Delete delete = new Delete(Bytes.toBytes("row1"));
      delete.deleteColumn(Bytes.toBytes("personal"), Bytes.toBytes("name"));
      delete.deleteFamily(Bytes.toBytes("professional"));

      // deleting the data
      table.delete(delete);

      // closing the HTable object
      table.close();
      System.out.println("data deleted.....");
   }
}
```
