## Exit

To exist the shell you should type the exit command

``` Java
> exit
```

## Stopping HBase

To stop HBase, browse to the HBase home folder and type the following command

``` Java
./bin/stop-hbase.sh
```

## Stopping HBase Using Java API

You can shut down the HBase using the **shutdown()** method of the **HBaseAdmin** class. Follow the steps given below to shut 
down HBase:

### Step 1

Instantiate the HbaseAdmin class.

``` Java
// Instantiating configuration object
Configuration conf = HBaseConfiguration.create();

// Instantiating HBaseAdmin object
HBaseAdmin admin = new HBaseAdmin(conf);
```

### Step 2

Shut down the HBase using the **shutdown()** method of the **HBaseAdmin** class.

``` Java
admin.shutdown();
```

### Complete program to stop the HBase.

``` Java
import java.io.IOException;

import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.client.HBaseAdmin;

public class ShutDownHbase{

   public static void main(String args[])throws IOException {

      // Instantiating configuration class
      Configuration conf = HBaseConfiguration.create();

      // Instantiating HBaseAdmin class
      HBaseAdmin admin = new HBaseAdmin(conf);

      // Shutting down HBase
      System.out.println("Shutting down hbase");
      admin.shutdown();
   }
}
```
