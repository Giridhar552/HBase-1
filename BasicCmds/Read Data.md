# Reading Data

The get command and the get() method of HTable class are used to read data from a table in HBase. Using get command, you can get a single row of data at a time. Its syntax is as follows:

``` Java
get '<table name>','row1'
```

### Reading a Specific Column

Below is the syntax to read a specific column

``` Java
hbase> get 'table name', ‘rowid’, {COLUMN ⇒ ‘column family:column name ’}
```

And example would be:

``` Java
hbase(main):015:0> get 'emp', 'row1', {COLUMN ⇒ 'personal:name'}
  COLUMN                CELL  
personal:name timestamp = 1418035791555, value = raju
1 row(s) in 0.0080 seconds
```

### Reading Data Using Java API

To read data from an HBase table, use the **get()** method of the HTable class. This method requires an instance of the **Get** class. 
Follow the steps given below to retrieve data from the HBase table.

### Step 1: Instantiate the Configuration Class

**Configuration** class adds HBase configuration files to its object. You can create a configuration object using the **create()** 
method of the **HbaseConfiguration** class as shown below.

``` Java
Configuration conf = HbaseConfiguration.create();
```

### Step 2: Instantiate the HTable Class

You have a class called **HTable**, an implementation of Table in HBase. This class is used to communicate with a single HBase table. 
While instantiating this class, it accepts the configuration object and the table name as parameters. You can instantiate the HTable 
class as shown below.

``` Java
HTable hTable = new HTable(conf, tableName);
```

### Step 3: Instantiate the Get Class

You can retrieve data from the HBase table using the **get()** method of the HTable class. This method extracts a cell from a given row. 
It requires a **Get** class object as parameter. Create it as shown below.

``` Java
Get get = new Get(toBytes("row1"));
```

### Step 4: Read the Data

While retrieving data, you can get a single row by id, or get a set of rows by a set of row ids, or scan an entire table or a subset 
of rows.

You can retrieve an HBase table data using the add method variants in **Get** class.

To get a specific column from a specific column family, use the following method.

``` Java
get.addFamily(personal) 
```

To get all the columns from a specific column family, use the following method.

``` Java
get.addColumn(personal, name) 
```

### Step 5: Get the Result

Get the result by passing your **Get** class instance to the get method of the **HTable** class. This method returns the **Result** class 
object, which holds the requested result. Given below is the usage of **get()** method.

``` Java
Result result = table.get(g);  
```

### Step 6: Reading Values from the Result Instance

The **Result** class provides the **getValue()** method to read the values from its instance. Use it as shown below to read the values 
from the **Result** instance.

``` Java
byte [] value = result.getValue(Bytes.toBytes("personal"),Bytes.toBytes("name"));
byte [] value1 = result.getValue(Bytes.toBytes("personal"),Bytes.toBytes("city"));
```


### Complete program to Read Data

``` Java
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.client.Get;
import org.apache.hadoop.hbase.client.HTable;
import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.util.Bytes;

public class RetriveData{

   public static void main(String[] args) throws IOException, Exception{
   
      // Instantiating Configuration class
      Configuration config = HBaseConfiguration.create();

      // Instantiating HTable class
      HTable table = new HTable(config, "emp");

      // Instantiating Get class
      Get g = new Get(Bytes.toBytes("row1"));

      // Reading the data
      Result result = table.get(g);

      // Reading values from Result class object
      byte [] value = result.getValue(Bytes.toBytes("personal"),Bytes.toBytes("name"));

      byte [] value1 = result.getValue(Bytes.toBytes("personal"),Bytes.toBytes("city"));

      // Printing the values
      String name = Bytes.toString(value);
      String city = Bytes.toString(value1);
      
      System.out.println("name: " + name + " city: " + city);
   }
}
```
